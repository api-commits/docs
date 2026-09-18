# Bit2Me API documentation

Mintlify developer portal for the Bit2Me gateway, Pro Trading, partner journeys, WebSockets, and MCP.

This site runs **in parallel** with the Scalar reference at [api.bit2me.com/doc](https://api.bit2me.com/doc). There is no production cutover until Bit2Me approves it.

## Local preview

```bash
npm i -g mint
mint dev
```

Open [http://localhost:3000](http://localhost:3000).

## Checks

```bash
mint validate
mint broken-links
mint a11y
```

## Source of truth

| Path | Role |
| --- | --- |
| `openapi/crypto.json` | Wallet / gateway REST snapshot |
| `openapi/trading-spot-rest.json` | Pro REST |
| `openapi/embed.json` | Partner widgets session |
| `asyncapi/trading.yaml` | Pro WebSocket channels |
| `.raw-openapi/` | Raw gateway, money-flow, and WS OpenAPI dumps |
| `docs.json` | Navigation, Bit2Me chrome, Status/Support links |

Do not invent endpoints. HMAC algorithm and fixture: `guides/authentication.mdx`.

## Brand

Colors: primary `#0046E1`, dark `#001A33`. Logos from the [Bit2Me press kit](https://bit2me.com/press). Status: [status.bit2me.com](https://status.bit2me.com). Support: [support.bit2me.com](https://support.bit2me.com).

## Publishing

Install the Mintlify GitHub app on `api-commits/docs`. Preview stays off `api.bit2me.com` until cutover.
