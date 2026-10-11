# ElseMail FS — backend-only 6h host for `fs.elsemail.indevs.in`

GitHub Actions diye backend host (proti run max ~6h). Shudhu backend, kono
frontend build nai. `fs` domain-e **API + `/health` only** — pages 404
(`src/index.js` host split). Full access: header `x-api-key: <SERVICE_API_KEY>`.

## Secrets (repo Settings -> Secrets and variables -> Actions)

| Name | Ki |
|---|---|
| `CF_TUNNEL_TOKEN_FS` | `elsemail-fs` Cloudflare Tunnel token (JWT) |
| `SERVICE_API_KEY` | FS backend-er root API key |
| `DKIM_PRIVATE_PEM` | DKIM private key (optional, unsigned chara mail jabe) |

## Run

Actions -> `ElseMail FS host (6h)` -> Run workflow. Live check:

```bash
curl https://fs.elsemail.indevs.in/health
curl -H "x-api-key: <SERVICE_API_KEY>" https://fs.elsemail.indevs.in/api/auth/check
```

## Notes

* Runner-e outbound port 25 pray block thake — direct-to-MX fail korte pare.
  Mail accept + archive hobe, dekho `GET /api/console/mails`.
* OTP/token memory-te thake — PC backend ar FS backend alada instance, code
  jekhane issue sekhanei verify korte hobe.
* Tunnel: `elsemail-fs` (Cloudflare dashboard -> Zero Trust -> Networks).
  DNS `fs.elsemail.indevs.in` CNAME tunnel-er dike, ingress `-> :3000`.
