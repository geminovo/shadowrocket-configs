# Changelog

All notable changes to this config are documented here.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

- AdGuard Home DoH external exposure (see ROADMAP.md P1)
- Additional AI domain rules (Gemini, Perplexity, Grok)

---

## [1.2.0] - 2026-06-07

### Fixed
- Added `raw.githubusercontent.com` to `skip-proxy` — prevents VPN interference when Shadowrocket auto-updates config

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
