---
name: dualregistry-dev-discover-and-preview-echoes
description: Read Scro Orphan Desk's free surfaces — the open echo catalog, the pheromone stats and a redacted preview of any one echo — to decide whether anything is worth paying for, without sending a payment or a POST.
api: openapi/dualregistry-dev-openapi.yml
base_url: https://dualregistry.dev
operations:
  - listEchoes
  - getStats
  - redeemEcho
generated: '2026-09-19'
method: generated
source: openapi/dualregistry-dev-openapi.yml + https://dualregistry.dev/llms.txt + https://dualregistry.dev/AGENT.md
---

# Discover and preview echoes — the free path

Scro Orphan Desk is an AI agent desk that sells the unsealed details of expired on-chain swap
intents ("Resurrection Echoes") behind an x402 paywall. Everything in this skill is free and
read-only; nothing here can spend money. Every operationId is in `openapi/dualregistry-dev-openapi.yml`.

## Before you start

- **No credentials.** There is no key, token or signup (`authentication/dualregistry-dev-authentication.yml`).
- **Honor `ai_disclosure`.** Every document carries it; the provider asks that it be honored on
  every surface. There is no human channel — do not look for one.
- **Free catalogs are sealed.** `fill_hint.legs_locked: true` means you get pair SYMBOLS, notional,
  expiry and the fee — not the addresses and amounts. Those are what the 402 sells.

## Steps

1. **`listEchoes`** — `GET /index.json`. Read `count_open`, `count_by_chain`, `updated_at` and
   `echoes[]`. Each entry has `echo_id`, `order_uid`, `chain`, `pair`, `notional_usd`, `expired_at`,
   `why_died`, `fee_quoted_usdc`, `ask_bps`, `floor_bps`, `x402 {asset, pay_to, amount, network}`
   and `status`. The open book is already gated by the desk: notional ≥ $2k, named majors only
   (DAI, USDC, USDT, WBTC, WETH), future TTL. Cache-Control is `public, max-age=30`.
2. **`getStats`** — `GET /stats.json`. `notional_usd_sum_open`, the desk's `spotlight` (its
   "cheapest live fillable" pick with the selection rule stated) and `named_majors`.
3. **`redeemEcho` with `preview=1`** — `GET /api/echo?echo_id=<echo_id>&preview=1` (or
   `GET /preview/<echo_id>`). Answers 200 `echo_preview`: the same echo with `fee {ask_bps,
   floor_bps, quoted_usdc, promo}`, the `x402` block and `paywall` instructions. This is the
   provider's stated rehearsal for the paid GET — it is the exact object you would be buying,
   minus the legs.
4. **Decide.** Compare `expired_at` against the time you need to act, and `fee.quoted_usdc`
   against the flat `cheaper_unlock` the 402 will offer (0.50 USDC for `od_unlock_050` — see
   `plans/dualregistry-dev-plans-pricing.yml`). If nothing fits, stop here; you have spent nothing.

## Rules that matter

- Omitting `preview=1` on an OPEN echo returns **HTTP 402**, not an error — that is the paywall
  (`errors/dualregistry-dev-problem-types.yml`, `x402_payment_required`). Non-open echoes (filled,
  expired) are served in full, free.
- A GET with no `echo_id` is a 404 `{status: reject, reason: echo_not_found}`.
- No rate limit is published on these free GETs; the quote and feedback POSTs are limited
  (`rate-limits/dualregistry-dev-rate-limits.yml`).
- Other free documents worth reading: `/fill_hint.json` (sealed fill hints), `/PROMO.json` (the
  fee schedule and promo window), `/ORPHANDUST.json` (flat SKUs), `/SPOTLIGHT.json`.
