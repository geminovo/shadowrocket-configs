# Git Naming Conventions (2026)

## Branch Naming

Format: `<type>/<short-description>` or `<type>/<TICKET-ID>-short-description`

| Prefix | Use Case | Example |
|---|---|---|
| `feature/` | New feature | `feature/add-claude-rules` |
| `fix/` | Bug fix | `fix/dns-leak-on-direct` |
| `hotfix/` | Urgent production patch | `hotfix/PROJ-42-proxy-crash` |
| `refactor/` | Code restructure | `refactor/split-rule-groups` |
| `docs/` | Documentation only | `docs/update-readme` |
| `chore/` | Maintenance, deps, tooling | `chore/update-surfshark-endpoint` |
| `test/` | Test additions | `test/add-dns-validation` |
| `release/` | Release prep | `release/1.2.0` |

**Rules:**
- Lowercase + hyphens only (`feature/add-user`, NOT `feature/addUser`)
- 3–5 words max after the prefix
- Include ticket ID when using issue tracker (`fix/GH-23-broken-rule`)
- No special characters: `!@#$%^&*`
- Never use ambiguous names: `update`, `test`, `changes`, `stuff`

---

## Commit Messages (Conventional Commits)

Format: `<type>(<optional scope>): <description>`

```
feat(rules): add claude.ai domain to AI proxy group
fix(general): correct dns-server fallback order
docs(readme): document proxy group naming
chore(deps): update surfshark wireguard endpoint
refactor(rules): split AI and streaming rule groups
perf(dns): reduce hijack-dns list overhead
test(config): validate tun-excluded-routes range
revert: revert "feat(rules): add gemini domains"
```

| Type | When to Use |
|---|---|
| `feat` | New feature or rule |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `chore` | Maintenance, no logic change |
| `refactor` | Restructure, no behavior change |
| `perf` | Performance improvement |
| `test` | Adding/updating tests |
| `ci` | CI/CD pipeline changes |
| `revert` | Reverting a previous commit |

**Rules:**
- Imperative mood: `add`, `fix`, `update` (NOT `added`, `fixed`)
- No period at end of subject line
- Subject line ≤ 72 characters
- Breaking changes: add `BREAKING CHANGE:` footer or `!` after type: `feat!: drop ipv6 support`

---

## Tag / Release Versioning (SemVer)

Format: `v<MAJOR>.<MINOR>.<PATCH>`

```
v1.0.0   → initial stable release
v1.1.0   → new feature added (backward compatible)
v1.1.1   → bug fix
v2.0.0   → breaking change
```

| Segment | Bump When |
|---|---|
| MAJOR | Breaking / incompatible changes |
| MINOR | New backward-compatible features |
| PATCH | Backward-compatible bug fixes |

**Rules:**
- Always prefix with `v` for git tags
- Annotated tags for releases: `git tag -a v1.0.0 -m "Release v1.0.0"`
- Pre-release: `v1.0.0-alpha.1`, `v1.0.0-beta.2`, `v1.0.0-rc.1`

---

## PR / Issue Title Convention

Mirror Conventional Commits format:
```
feat(proxy): add Gemini AI domains to AI group
fix(rules): remove duplicate DOMAIN-SUFFIX entries
docs: add subscription URL instructions
```

---

## Quick Reference Summary

```
Branch:  feature/add-gemini-rules
Commit:  feat(rules): add gemini.google.com to AI group
Tag:     v1.2.0
PR:      feat(rules): add Gemini AI domains
```
