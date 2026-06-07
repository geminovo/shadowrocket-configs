# shadowrocket-configs

Private Shadowrocket proxy configurations for iOS.

## Active Config

**[`active.conf`](./active.conf)** — always the current version in use.

### DNS Strategy

| Network | DNS | AdGuard |
|---|---|---|
| Home WiFi | `192.168.50.16` (AdGuard Home) | ✅ Active |
| Outside / 4G | Fallback DoH `1.1.1.1` / `8.8.8.8` | ❌ Not active |

> AdGuard Home upstream: Quad9 + Cloudflare + Google (all DoH encrypted)

### Proxy Groups

| Group | Proxy | Covers |
|---|---|---|
| `AI` | `TW-Surfshark-WG` | OpenAI, Claude, NotebookLM |

## Structure

```
├── active.conf       # Current config — load this in Shadowrocket
├── CHANGELOG.md      # What changed and why
├── ROADMAP.md        # Pending improvements
└── archive/          # Previous versions
```

## Pending

See [ROADMAP.md](./ROADMAP.md) for planned improvements.
