# Changelog

All notable changes to this config are documented here.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

- AdGuard Home DoH external exposure (see ROADMAP.md P1)

---

## [1.2.3] - 2026-06-11

### Fixed
- Added `bypass-system = true` — system-level traffic (APNs, NTP, iCloud) now routes through TUN, preventing carrier DNS exposure on cellular
- Removed `raw.githubusercontent.com` from `skip-proxy` — was bypassing Shadowrocket entirely, causing DNS queries to leak to system resolver

---

## [1.2.2] - 2026-06-11

### Fixed
- Merged `fallback-dns-server` into `dns-server` as parallel entries — eliminates timeout delay when roaming and `192.168.50.16` is unreachable

### Removed
- `fallback-dns-server` directive (consolidated into `dns-server`)

---

## [1.2.1] - 2026-06-11

### Added
- `DOMAIN,openaiassets.blob.core.windows.net,AI` — OpenAI Azure CDN domain missing from rules, was leaking to AdGuard/DIRECT

---

## [1.2.0] - 2026-06-07

### Fixed
- Added `raw.githubusercontent.com` to `skip-proxy` — prevents VPN interference when Shadowrocket auto-updates config
  *(reverted in 1.2.3 — skip-proxy bypasses DNS entirely, causing system resolver leak)*

---

## [1.1.0] - 2026-06-07

### Changed
- `dns-server` → `192.168.50.16` (AdGuard Home direct)
- `dns-direct-system` → `false`
- Removed `hijack-dns` — was overriding AdGuard Home DNS responses

### Fixed
- AdGuard Home blocked by Shadowrocket DNS hijack on home network

---

## [1.0.0] - 2026-06-07

### Added
- Initial config with AI proxy group → `TW-Surfshark-WG`
- Rules: OpenAI / ChatGPT, Claude / Anthropic, Google NotebookLM
- ChatGPT Voice / Realtime (LiveKit) domains
- OpenAI CDN and feature flag domains
- `block-quic = all-proxy` — prevent QUIC bypass
- `ipv6 = false` — prevent IPv6 leak
- `udp-policy-not-supported-behaviour = REJECT`
