# Documentation project instructions

This is the **Bit2Me API** developer portal (Mintlify). It is a parallel site to Scalar at https://api.bit2me.com/doc. Do not mix this work into the API Director git repo.

## About this project

- Pages are MDX with YAML frontmatter
- Configuration lives in `docs.json`
- OpenAPI snapshots live in `openapi/` — treat them as the REST source of truth
- Pro WebSocket channels: `asyncapi/trading.yaml`
- Run `mint dev` to preview locally
- Run `mint broken-links` and `mint validate` before announcing a preview

## Terminology

- Use **parent**, **subaccount**, and **pocket** (not “project” or “merchant wallet” unless the spec says so)
- Gateway host is `https://gateway.bit2me.com`
- HMAC headers: `x-api-key`, `api-signature`, `x-nonce`
- Subaccount header: `X-SUBACCOUNT-ID`
- Subaccount 2FA type is always `gauth`
- Pro WS: `wss://ws.bit2me.com/v1/trading` — token from `POST /v1/signin/apikey` (1 minute)
- Gateway notifications are a separate socket; do not invent the hostname if the spec uses a placeholder
- `bit2me-api-node-tool` is discontinued — not an SDK

## Style preferences

- English first; active voice; second person (“you”)
- Sentence case for headings
- One idea per sentence
- Bold for UI: Click **Settings**
- Code formatting for paths, headers, and commands
- Always-visible Status (`https://status.bit2me.com`) and Support (`https://support.bit2me.com`)
- Primary CTA is **Get API keys**, not Support

## Content boundaries

- Do not invent endpoints, SLAs, uptime %, sunset dates, address-book TTLs, or Travel Rule EUR thresholds
- Withdrawal networks, minimums, and fees come from `GET /v1/blockchain-manager/configuration/currency` (`https://gateway.bit2me.com`). The body is currency then network: each item has `symbol` and `networks[]` with `networkId`, `minimumWithdrawal`, and `withdrawalFee` (decimal strings). Pass `networkId` through as `network` on address-book and deposit-address calls. Do not publish a static fee table or map display names onto `networkId` (`polygon` and `polygonUsdc` are different ids). `GET /v2/currency/assets` is the asset catalog only (name, exponent, pairs) and does not return networks or withdrawal limits. This configuration route is **not** in the current `openapi/crypto.json` or `.raw-openapi/gateway.json` snapshot — do not hand-author it into the snapshot; it belongs in API Director first, then a snapshot refresh. Until that lands, guide copy may name the call and point at the live response.
- Travel Rule on the address-book path is the entry itself (`walletType`, `walletOwnership`, `exchangeName`). Do not call `POST /v2/blockchain-manager/travel-rule-order/{orderId}` after an address-book draft. That POST is Wallet legacy only, and only when the confirmed proforma operation status is `pending_user_information`. `{orderId}` is the operation id, not the proforma id. Do not invent EUR thresholds or cancel TTLs.
- There is **no sandbox**. Production hosts only (`gateway.bit2me.com`, `embed.bit2me.com`).
- Social Pay (OpenAPI **Transfers**) is the rail to another Bit2Me user (`email` / `phone` / `alias`). Last-mile fiat is Argentina only. On-chain to an external wallet is address book, not Social Pay.
- Do not document `internal` notification channel as stable
- Futures WS is limited availability until product/legal sign-off
- No partner names, user IDs, or Jira keys on customer pages
- Playground stays **simple** — Mintlify cannot compute HMAC-SHA512
- KYC, KYB, Travel Rule, and 2FA pages require Legal/Compliance review before partner announcement (`COMPLIANCE_BLOCKER` until that sign-off)

## Mintlify

For Mintlify product knowledge, use the Mintlify skill: `npx skills add https://mintlify.com/docs`
