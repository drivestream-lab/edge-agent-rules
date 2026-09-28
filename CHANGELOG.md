# Changelog

All notable changes to `edge-agent-rules` are documented here.

Format: **Breaking** changes require code changes in consumer repos before or alongside the version bump. **Additive** changes are safe to adopt incrementally.

---

## v0.2.0

### Summary

Craft-only pressure-test: remove Autrio/product topology from constitution.
Rename OTA-framed reconcile to desired-state; MQTT and identity no longer
require the agent to own device-root cloud session or join secrets. DI
singleton wording aligned with `python-services-rules`.

### Breaking

- Renamed **`ota-reconciliation.mdc`** → **`desired-state-reconciliation.mdc`**
  (update consumer docs / ADR cross-links that cited the old filename)
- **`mqtt-transport.mdc`**: no longer states the agent must own one broker
  client for both planes as device-root gateway — protocol defaults remain;
  ownership is consumer ADR
- **`device-identity-security.mdc`**: focuses on on-device verify + secrets
  hygiene; device-root credential holder is consumer ADR

### Additive

- README: preferred scaffold `edge-agent-foundation`; Triton foundation as variant
- Cross-links to `python-services-rules` for shared DI/singleton practice
- **`resource-governance.mdc`**: do not invent host disk topology when host
  authority supplies paths

### Migration guide

- Pin `v0.2.0`; replace references to `ota-reconciliation.mdc`
- Document device-root MQTT / identity ownership in product ADRs (not here)
- No required Python API renames from this bump alone

---

## v0.1.0

### Summary

Initial constitution for Edge Agent services — two-plane doctrine, dual buffers, OTA reconciliation, engine contract, and Python craft adapted for a long-running agent. Package layout is **`business_services/` + `infra_services/`** with explicit `*_service` naming (planes are conceptual, not folders).

### Changes

- Initial module set (see `code-guidelines-index.mdc`)
- MIT license, versioned submodule adoption pattern

### Migration guide

- Greenfield: mount this repo at `.cursor/rules` and pin `v0.1.0`
- No prior consumers
