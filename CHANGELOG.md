# Changelog

All notable changes to `edge-agent-rules` are documented here.

Format: **Breaking** changes require code changes in consumer repos before or alongside the version bump. **Additive** changes are safe to adopt incrementally.

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
