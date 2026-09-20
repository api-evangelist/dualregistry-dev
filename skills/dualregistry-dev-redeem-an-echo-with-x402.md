---
name: dualregistry-dev-redeem-an-echo-with-x402
description: Redeem one open echo through Scro Orphan Desk's x402 paywall — pick it from the free index, optionally negotiate the finder's fee with an exploratory then firm quote, pay the 402 invoice in USDC on Base, retry the GET with payment-proof headers, and receive the unsealed legs plus a receipt. Stops at every point where money would move.
api: openapi/dualregistry-dev-openapi.yml
base_url: https://dualregistry.dev
operations:
  - listEchoes
  - redeemEcho
  - quoteFee
  - settleFee
generated: '2026-09-19'
method: generated
source: openapi/dualregistry-dev-openapi.yml + https://dualregistry.dev/llms.txt ("Per-Echo GET (x402 paywall)", "OBO→pay") + the agent card `redeem` skill flow[] + the live 402 body observed 2026-09-19
---

# Redeem an echo with x402

This is the provider's own "one-shot redeem" flow, from the agent card:
`GET /index.json → pick echo_id → optional POST /api/quote_fee → pay USDC on Base (or USDT on BSC)
→ GET /api/echo?echo_id=… with X-PAYMENT-TX + X-PAYMENT-CHAIN → receive full echo + receipt`.
Every operationId is in `openapi/dualregistry-dev-openapi.yml`.

## Read this first — reversibility is NONE

The payment is an on-chain stablecoin transfer to the desk's receive wallet. There is no cancel,
refund, void or undo anywhere on this API (`conventions/dualregistry-dev-conventions.yml`,
`reversibility.grade: none`). Quotes expire (20 minutes) and invoices time out (600 s), but an
expiry is not a reversal. Decide before you pay, and pay once.

## Steps

1. **`listEchoes`** — `GET /index.json`; choose an `echo_id` whose `expired_at` gives you time.
   Preview it free first: `GET /api/echo?echo_id=<id>&preview=1` (skill *discover-and-preview*).
2. **Optional — `quoteFee`, exploratory.** `POST /api/quote_fee` with
   `{"echo_id": "<id>", "bid_bps": <n>}` and `firm` omitted or false → **200 indicative**
   `ask_bps` / `floor_bps` (request and response shapes in
   `json-schema/dualregistry-dev-fee-quote.schema.json`). Free; no commitment. Limit: 10 per 10
   minutes per IP+User-Agent → 429 + `Retry-After`.
3. **Optional — `quoteFee`, firm.** Same body with `"firm": true` (`quote_bond_usdc` is 0):
   `bid_bps >= ask_bps` → **402 accept invoice** with `quote_id`, `final_usdc` and `expires_at`;
   `floor <= bid < ask` → 200 counter (`counter_rule: midpoint_ceil`); `bid < floor` → 422.
   A firm accept is the price you are agreeing to; it binds for 20 minutes.
4. **`redeemEcho`, unpaid** — `GET /api/echo?echo_id=<id>` → **HTTP 402** `x402_payment_required`.
   Read `accepts[0]` (scheme `exact`, network `eip155:8453`, USDC asset
   `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, `payTo`, `maxAmountRequired` in 6-decimal units,
   `maxTimeoutSeconds` 600) and `amount` (the fee in USDC, e.g. `"2.49"` = 10 bps of a $2,491
   echo). Note `cheaper_unlock`: if `od_unlock_050` at 0.50 USDC is less than the fee, the desk
   itself recommends it (skill *buy-an-orphandust-unlock*). The same invoice is base64 in the
   `PAYMENT-REQUIRED` response header.
5. **Pay — outside this API.** Transfer exactly `amount` USDC on Base to `payTo` (USDT on BSC, or
   USDC/USDT on Ethereum, are listed in `accepted[]`). **This is the irreversible step.** Keep the
   transaction hash.
6. **`redeemEcho`, with proof** — repeat the SAME GET with headers `X-PAYMENT-TX: 0x…` and
   `X-PAYMENT-CHAIN: base` (optional `X-PAYMENT-ASSET`, `X-PAYMENT-AMOUNT`, and `X-QUOTE-ID` if you
   hold a firm quote). Query `?tx_hash=&chain=` is equivalent. The server RPC-verifies the ERC-20
   Transfer ("fail-closed"), auto-runs settle_fee, and answers 200 with the full echo — unsealed
   `sell`/`buy` legs (address, amount, decimals), executable `fill_hint` — and a `receipt`.
7. **`settleFee`, only if step 6 did not settle** — `POST /api/settle_fee` with
   `{"quote_id" | "echo_id", "tx_hash", "chain", "amount_usdc", "asset"?: "USDC"|"USDT"}` → 200
   receipt (`fee.asset`, `fee.collected_usd`, `fee.chain`, `fee.tx_hash`). Same on-chain
   verification. `invalid_tx_hash` / `missing_echo_id` are 400s.
8. **Tell the desk what happened** — `POST /api/feedback` (documented, not in the spec)
   `{"agent_id", "stage": "fill", "outcome": "filled_ok", "echo_id"}` — or, if you walked away
   at step 4, `{"stage": "paywall_402", "outcome": "too_expensive"}`. 5 per 10 minutes.

## Idempotency and retries

- There is no idempotency key (`conventions/…`, `idempotency.coverage: none`). Treat every POST
  as at-most-once. A firm quote that timed out may still exist — do not re-fire it blindly.
- If step 6 fails after you paid, do not pay again: the proof is the tx hash, and the manual
  `settleFee` path accepts the same hash. Refusal reasons `quote_expired`, `quote_amount_mismatch`,
  `quote_asset_mismatch` come from a stale or mismatched `X-QUOTE-ID` — drop the header and retry
  the GET with the tx proof alone.
