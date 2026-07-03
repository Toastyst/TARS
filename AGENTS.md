# TARS — Agent Project Context

Trail Assistance & Reasoning System. Hermes profile: `tars` (from `Toastyst/tars-agent`).

## Architecture

See [design/TARS-DESIGN.md](design/TARS-DESIGN.md) for the full system design (July 2026).

## Layer map (L0–L8)

| Layer | Capability | Status |
|-------|------------|--------|
| L0 | Identity (`SOUL.md` in tars-agent) | User-authored |
| L1 | Hermes Agent runtime | Active |
| L2 | LLM (OpenRouter) | Active |
| L3 | Voice (Hermes voice layer) | Deferred |
| L4 | Trip context (weather, search) | In progress |
| L5 | Group GPS (ATAK + Meshtastic) | Planned |
| L6 | Radio intel (GMRS/CB RAG pattern) | Planned |
| L7 | Vehicle (OBD2) | Planned |
| L8 | Hardware (Jeep brain) | Deferred |

## Conventions

- Persona lives in **tars-agent** `SOUL.md` only — not in this repo.
- Set `TARS_WORKSPACE` to this directory for Hermes `terminal.cwd`.
- SearXNG (when enabled): `http://127.0.0.1:8080`
- Salvaged bench reference: `tools/bench/` (not production runtime)

## Related repos

- `Toastyst/tars-agent` — private Hermes profile distribution
- `Toastyst/TARS_JEEP` — legacy (archive after migration)