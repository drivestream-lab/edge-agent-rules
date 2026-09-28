# edge-agent-rules

**Open constitution for Edge Agent services** — shared Cursor agent rules (`.mdc`)
for a Python agent that scrapes, buffers, and forwards telemetry (data plane) and
reconciles **desired-state** (control plane) on constrained edge devices.

Rules describe **how to code**. They do **not** contain product requirements,
tenant names, hardware SKUs, broker product choices, inference-engine product
choices, or device topology (e.g. who owns the cloud MQTT session) — those live
in each consumer repo under `docs/specification/` and in foundations.

Shared practices (DI, singleton, fail-fast, logging fields) align with
[`python-services-rules`](https://github.com/drivestream-lab/python-services-rules)
naming and intent where the craft overlaps.

| | |
|---|---|
| **License** | [MIT](LICENSE) |
| **Version** | see [`VERSION`](VERSION) (currently **0.2.0**) · [CHANGELOG](CHANGELOG.md) |
| **Mount path** | `.cursor/rules/` (git submodule) |
| **Scaffold** | Prefer engine-agnostic **`edge-agent-foundation`** when published; `edge-agent-triton-foundation` remains a Triton-flavored variant |

---

## Layout

This repository root **is** the contents of a consumer's `.cursor/rules/` directory:

```text
edge-agent-rules/
  VERSION
  README.md
  CHANGELOG.md
  code-guidelines-index.mdc    ← module index (start here)
  architecture.mdc
  two-plane-architecture.mdc
  mqtt-transport.mdc
  local-buffer-pattern.mdc
  offline-dtn-operation.mdc
  resource-governance.mdc
  desired-state-reconciliation.mdc
  deployment-manifest.mdc
  device-identity-security.mdc
  engine-contract.mdc
  dependency-injection.mdc
  edge-agent-adr.mdc
  …
```

Full module table: [`code-guidelines-index.mdc`](code-guidelines-index.mdc).

---

## Adoption

From the **consumer agent repo root**:

```bash
rm -rf .cursor/rules

git submodule add https://github.com/drivestream-lab/edge-agent-rules.git .cursor/rules
cd .cursor/rules && git checkout v0.2.0 && cd ../..

git add .gitmodules .cursor/rules
git commit -m "Add Edge Agent Cursor rules at .cursor/rules (v0.2.0)"
```

Cursor loads **`.cursor/rules/*.mdc`** automatically — no copy step.

---

## What this constitution is (and is not)

| In scope | Out of scope |
|----------|--------------|
| Two-plane transport doctrine (telemetry up, desired-state down) | Named broker / SoC / serving-runtime products |
| Disk-backed dual buffers, value-based eviction | Tenant ODD numbers, physical link names |
| Desired-state reconciliation + signed manifests | Product OTA campaign / layer ownership |
| Engine **contract** (metrics + hot-reload + active version) | Model architecture, training, accuracy |
| Resource governance across engines on one device | Cloud Kafka / analytics-store choices |
| MQTT **protocol** defaults when the agent owns a client | Sole device-root MQTT gateway requirement |
| Python craft (DI/singleton aligned with python-services-rules) | Product field catalogs (those → `docs/specification/`) |

Concrete stack defaults (e.g. Triton, Jetson, EMQX) belong in a **foundation**
and in that consumer's ADRs — not in this package.

---

## Related repositories

| Repo | Role |
|------|------|
| `edge-agent-foundation` | Engine-agnostic Edge Agent cookiecutter (preferred when published) |
| `edge-agent-triton-foundation` | Triton/Jetson/EMQX-flavored variant (Law 5) |
| `edge-triton-client-foundation` | Triton serving client that satisfies the engine contract |
| `python-services-rules` | FastAPI microservices constitution (different shape — do not mount here) |
| `rust-device-rules` | Rust device daemon constitution (different craft — do not mount here) |

---

## Governance

| Principle | Detail |
|-----------|--------|
| **Ownership** | Platform / architecture team owns this repo |
| **Consumers** | Pin a release tag — never fork or edit rules in product repos |
| **Changes** | Propose via PR here; consumers update the submodule pointer only |
| **Product truth** | Requirements, ADRs, as-built → `docs/specification/` per agent repo |
| **Do not** | `gitignore` `.cursor/rules` in consumers — breaks the pinned submodule |

---

## Release process (maintainers)

1. Branch `rules/<short-description>` — edit `*.mdc` at repo root; peer review required
2. Bump **`VERSION`** (semver) and **`CHANGELOG.md`**
3. Update version in this README header
4. PR → `develop` → `main`; tag and push:

```bash
git tag v0.2.0
git push origin v0.2.0
```

---

## License

MIT — see [LICENSE](LICENSE).
