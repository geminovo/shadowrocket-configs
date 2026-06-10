# Shadowrocket Config Roadmap

## Current Setup

- `dns-server = 192.168.50.16, 1.1.1.1 DoH, 8.8.8.8 DoH` — parallel query, fastest wins
- Home WiFi: AdGuard Home (`192.168.50.16`) responds first
- Outside home: DoH (`1.1.1.1`, `8.8.8.8`) responds, no timeout penalty
- `bypass-system = true` — system traffic routes through TUN

---

## Backlog

### 🟡 P1 — High Value

- [ ] **AdGuard Home DoH exposure**
  Expose AdGuard Home via HTTPS reverse proxy (Nginx/Caddy) with a domain/DDNS.
  Allows `dns-server = https://yourdomain/dns-query` — works everywhere, AdGuard ad-blocking active even when roaming.
  Requires: public IP or DDNS + SSL cert (Let's Encrypt).

- [ ] **Router DHCP DNS config**
  Set DHCP DNS option to `192.168.50.16` on home router.
  Ensures all LAN devices use AdGuard Home without manual config.

### 🔵 P2 — Nice to Have

- [ ] **Tailscale DNS-only mode**
  Install Tailscale on AdGuard Home LXC + phone.
  Use Tailscale to reach `192.168.50.16` from anywhere — AdGuard ad-blocking restored when roaming.
  ⚠️ Potential iOS VPN conflict with Shadowrocket — test before committing.

- [ ] **WireGuard split-tunnel back to homelab**
  Self-hosted WireGuard on PVE. DNS-only tunnel — routes only port 53 traffic through home.
  More control than Tailscale, requires public IP / port forwarding.

### ⚪ P3 — Future Consideration

- [ ] **Per-SSID proxy profile switching**
  Use Shadowrocket SSID rules to load different configs at home vs outside.
  Useful if DNS strategy differs by network.

---

## Decisions Log

| Date | Decision | Reason |
|---|---|---|
| 2026-06-11 | Added `bypass-system = true` | Prevent system-level DNS leaking to carrier on cellular |
| 2026-06-11 | Removed `raw.githubusercontent.com` from `skip-proxy` | skip-proxy bypasses DNS entirely → system resolver leak |
| 2026-06-11 | Merged fallback into `dns-server` | Parallel query eliminates roaming timeout delay |
| 2026-06-07 | Removed `hijack-dns` | Was overriding AdGuard Home DNS responses |
| 2026-06-07 | Deferred Tailscale | iOS VPN conflict risk with Shadowrocket |
| 2026-06-07 | Removed streaming ruleset | Not a planned feature |
