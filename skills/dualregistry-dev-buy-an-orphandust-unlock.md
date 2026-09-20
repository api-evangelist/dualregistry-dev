---
name: dualregistry-dev-buy-an-orphandust-unlock
description: Buy one flat-priced OrphanDust unlock credit (od_unlock_050, 0.50 USDC on Base) from Scro Orphan Desk through its x402 402, then spend the credit to unseal one open echo instead of paying the basis-point finder's fee. Stops before the payment and explains what it commits you to.
api: openapi/dualregistry-dev-openapi.yml
base_url: https://dualregistry.dev
operations:
  - getOrphanDustInvoice
  - buyOrphanDustCredits
  - redeemEcho
generated: '2026-09-19'
method: generated
source: openapi/dualregistry-dev-openapi.yml + https://dualregistry.dev/ORPHANDUST.json + https://dualregistry.dev/.well-known/x402 + the live 402 bodies observed 2026-09-19 on /api/orphandust/buy and /api/echo (cheaper_unlock)
---

# Buy an OrphanDust unlock and spend it

OrphanDust is the desk's "preferred door": a flat 0.50 USDC per echo instead of a percentage fee.
The desk's own 402 on a per-echo GET recommends it (`cheaper_unlock`) whenever it is cheaper
than the quoted fee. Every operationId is in `openapi/dualregistry-dev-openapi.yml`; the unlock
step (`POST /api/orphandust/unlock`) is documented by the provider but absent from the served spec.

## Read this first

- **Reversibility: none.** A bought credit is not refundable; a spent credit is not un-spendable
  (`conventions/dualregistry-dev-conventions.yml`). Credits can expire (`credit_expired` exists as
  a refusal; the TTL is not published) — buy when you are ready to spend.
- **Prefer `od_unlock_050`.** The provider says so in the catalog: `od_credits_1` is the same one
  credit for $1.00, and the $3 / $5 packs are "demoted (worse per credit)".

## Steps

1. **Read the catalog (free)** — `GET /ORPHANDUST.json` (or `/PRODUCT.json`): `skus[]` with
   `sku`, `price_usdc`, `credits`, `preferred`, plus `preferred {asset USDC, network base,
   chain_id 8453, token}` and `also_accepts {USDT, bsc}`. The same SKU is declared in
   `/.well-known/x402` `resources[0]` (`priceUsd "0.50"`).
2. **`getOrphanDustInvoice`** — `GET /api/orphandust/buy` → **HTTP 402** `x402_payment_required`
   for `od_unlock_050`: `amount "0.50"`, `accepts[]` (scheme exact, `eip155:8453`, USDC
   `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, `maxAmountRequired "500000"`, `payTo`,
   `maxTimeoutSeconds 600`) and `unlock_after_pay {retry_post, body {sku}, headers}`. The POST
   form, `buyOrphanDustCredits` with `{"sku": "od_unlock_050"}`, answers the same 402 unpaid.
3. **Pay — outside this API.** Transfer 0.50 USDC on Base to `payTo`. **Irreversible.** Keep the
   transaction hash.
4. **`buyOrphanDustCredits`, with proof** — `POST /api/orphandust/buy` `{"sku": "od_unlock_050"}`
   with headers `X-PAYMENT-TX: 0x…` and `X-PAYMENT-CHAIN: base` (optional `X-PAYMENT-ASSET`,
   `X-PAYMENT-AMOUNT`). The server verifies the transfer on-chain and answers 200 with your
   credits and a `credit_token` (prefix `odc_`).
5. **Spend the credit — one of two documented ways:**
   - `POST /api/orphandust/unlock` `{"echo_id": "<id>", "credit_token": "odc_…"}` → the full echo
     legs ("consumes 1 unlock credit"); or
   - **`redeemEcho`** — `GET /api/echo?echo_id=<id>&credit_token=odc_…` (or header
     `X-CREDIT-TOKEN`) → 200 full echo.
   Refusals: `invalid_credit_token`, `credit_expired`, `credit_exhausted`.
6. **Feedback (documented, optional)** — `POST /api/feedback` with `stage: fill, outcome:
   filled_ok` — or, if you skipped the buy at step 2, `{stage: paywall_402, outcome:
   too_expensive}`, which is what the 402's `skip_feedback` block asks for. Never invent a human
   channel; there is none.

## Choosing between this and the fee path

Compare `cheaper_unlock.save_usdc` on the echo's 402 (skill *redeem-an-echo-with-x402*, step 4):
it is the quoted percentage fee minus 0.50. On a $2,491 echo at 10 bps the fee is 2.49 USDC and
the credit saves 1.99; on an echo whose fee is at the 0.25 promo floor the credit costs more.
