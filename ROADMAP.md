# Shadowrocket Config Roadmap

## Current Setup

- `dns-server = system` — relies on router DHCP to push AdGuard Home (`192.168.50.16`) at home
- Outside home: fallback to DoH (`1.1.1.1`, `8.8.8.8`)
- AdGuard Home only active on home WiFi

---

## Backlog

### 🟡 P1 — High Value

- [ ] **AdGuard Home DoH exposure**
  Expose AdGuard Home via HTTPS reverse proxy (Nginx/Caddy) with a domain/DDNS.
  Allows `dns-server = https://yourdomain/dns-query` — works everywhere, no VPN needed.
  Requires: public IP or DDNS + SSL cert (Let's Encrypt).

- [ ] **Router DHCP DNS config**
  Set DHCP DNS option to `192.168.50.16` on home router.
  Required for current `dns-server = system` strategy to work at home.
  Without this, system DNS won't point to AdGuard Home.

### 🔵 P2 — Nice to Have

- [ ] **WireGuard split-tunnel back to homelab**
  Self-hosted WireGuard on PVE. DNS-only tunnel — routes only port 53 traffic through home.
  More control than Tailscale, requires public IP / port forwarding.

- [ ] **Tailscale DNS-only mode**
  Install Tailscale on AdGuard Home LXC + phone.
  Use Tailscale as DNS-only (no exit node) to reach `192.168.50.16` from anywhere.
  ⚠️ Potential iOS VPN conflict with Shadowrocket — test before committing.

### ⚪ P3 — Future Consideration

- [ ] **Per-SSID proxy profile switching**
  Use Shadowrocket SSID rules to load different configs at home vs outside.
  Useful if DNS strategy differs by network.

- [ ] **Separate streaming ruleset**
  Extract Netflix / Disney+ / YouTube rules into dedicated proxy group.
  Allows independent proxy selection for streaming vs AI.

---

## Decisions Log

| Date | Decision | Reason |
|---|---|---|
| 2026-06-07 | Removed `hijack-dns` | Was overriding AdGuard Home DNS responses |
| 2026-06-07 | `dns-server = system` | Let router DHCP control DNS per network environment |
| 2026-06-07 | Deferred Tailscale | iOS VPN conflict risk with Shadowrocket |
