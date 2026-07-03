# TARS — Trail Assistance & Reasoning System

Voice-first trail companion for off-road and road-trip use. Runtime: [Hermes Agent](https://hermes-agent.nousresearch.com/) with a dedicated `tars` profile.

## Repos

| Repo | Role |
|------|------|
| **[TARS](https://github.com/Toastyst/TARS)** (this repo) | Project workspace — `AGENTS.md`, docker, tools, docs |
| **[tars-agent](https://github.com/Toastyst/tars-agent)** | Private Hermes profile — `SOUL.md`, skills, config |
| **[TARS_JEEP](https://github.com/Toastyst/TARS_JEEP)** | Legacy prototype (archiving after migration) |

## Design

Full system design: [design/TARS-DESIGN.md](design/TARS-DESIGN.md)

## Quick start (planned)

```powershell
hermes profile install github.com/Toastyst/tars-agent --alias
# Configure ~/.hermes/profiles/tars/.env (OPENROUTER_API_KEY, TARS_WORKSPACE)
git clone https://github.com/Toastyst/TARS C:\TARS
tars config set terminal.cwd C:/TARS
cd C:\TARS
tars chat
```

Setup guide: `docs/hermes-setup.md` (coming in PR-11).

## Status

July 2026 — design approved; implementing PR-1 through PR-11. Text-first on MacBook Boot Camp; voice and Jeep hardware layers deferred.