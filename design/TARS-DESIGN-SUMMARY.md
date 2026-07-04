# TARS System Design Summary — July 2026

**Full document:** [design/TARS-DESIGN.md](TARS-DESIGN.md)  
**Status:** Revised — post-review Pass 2 (90cbc947); implementation update **2026-07-04**  
**Date:** 2026-07-03 (design)

---

## One-liner

TARS is a **Hermes Agent–powered, voice-first trail companion** for Jeep off-road use — migrating from `tars_test_bench.py` / `TARS_JEEP` prototypes into a **two-repo architecture** (`tars-agent` private profile + `TARS` public workspace) with trip-context skills first, hardware layers later.

---

## What changes

| Before | After |
|--------|-------|
| Monolithic `tars_test_bench.py` (local, no git) | Hermes `tars` profile via `hermes profile install` |
| `TARS_JEEP` nested artifact + committed DBs | Clean `TARS` repo; `TARS_JEEP` archived **after mandatory DB history purge** |
| System prompt in Python (`SYSTEM_PROMPT`) | User-owned `SOUL.md` in `tars-agent` |
| Ollama + Open WebUI stack | OpenRouter (dev) + Hermes skills + SearXNG docker (pipelines dropped) |
| No layer structure | L0–L8 capability map |
| Whole-workspace `git add .` risk | PR-1 explicit allow-list; gitignore `mcps/`, `.design/`, etc. |

---

## Architecture (compressed)

```
tars-agent (private)          TARS (public workspace)
├── SOUL.md (persona)         ├── AGENTS.md (project context)
├── config.yaml (Hermes schema)│   terminal.cwd via TARS_WORKSPACE
│   model.provider, platform_toolsets ├── docker/searxng/ (127.0.0.1 only)
├── distribution.yaml         ├── tools/voice/ (reference)
└── skills/                   └── design/ (committed from .design/)
    ├── weather + geocode script
    ├── trail-search + search.py
    └── trip-plan (post-v0.1)
         │
         ▼
    Hermes Agent → OpenRouter LLM
```

**July 2026 focus:** L0 (SOUL) + L1 (Hermes) + L2 (OpenRouter) + L4 (weather w/ Nominatim geocode, trail-search).  
**Deferred:** L3 Hermes voice (Phase 2), L5–L8 hardware layers.

---

## Key decisions (11)

1. Hermes Agent = sole runtime
2. Two repos: `tars-agent` + `TARS`
3. Text-first dev (Boot Camp mic unreliable)
4. User-authored `SOUL.md` — verify overwrites Hermes default seed
5. L4 trip context before hardware layers
6. Salvage TARS_JEEP, don't evolve in place
7. OpenRouter until local inference on Jeep hardware
8. ATAK for group GPS; Meshtastic as mesh
9. No general local RAG/KB (L6 radio-only later)
10. Archive TARS_JEEP **after mandatory** DB history purge
11. **`TARS` public**; `tars-agent` private

---

## Implementation progress (Jul 2026)

| Done | Deferred / pending |
|------|-------------------|
| PR-1 TARS scaffold, PR-3 design docs | PR-2 `tars-agent` + Hermes install |
| PR-10 partial: Pokemon cluster, emote stub | PR-4–8 skills, bench, voice, SearXNG |
| `TARS` public on GitHub | `TARS_JEEP` archive (after DB purge) |

Hermes profile install and OpenRouter smoke test **deferred** — limited time/budget.

---

## PR plan — 12 PRs

| PR | Title | Repo | Status |
|----|-------|------|--------|
| 1 | Initialize TARS scaffold (**allow-list only**) | TARS | **Done** |
| 2 | Bootstrap Hermes profile + **config.yaml** (`0.0.1`) + smoke test | tars-agent | **Deferred** |
| 3 | Add design docs → `design/` | TARS | **Done** |
| 4 | Migrate **local OpenRouter** bench | TARS | Pending |
| 5 | Salvage voice module | TARS | Pending |
| 6 | SearXNG docker (**localhost bind**, no pipelines) | TARS | Pending |
| 7 | weather + trail-search scripts | tars-agent | Pending |
| 8 | User-authored SOUL.md v0.1 | tars-agent | Pending |
| 9 | Scaffold L5/L6/L7/L8 plugin docs | TARS | Pending |
| 10 | GitHub cleanup | GitHub | **Partial** (Pokemon + emotes done; TARS_JEEP pending) |
| 11 | Hermes setup docs | TARS | Pending |
| 12 | trip-plan stub *(post-v0.1)* | tars-agent | Pending |

**Critical path:** PR-1 ✅ → PR-2 (smoke) → PR-6 → PR-7 → PR-8 → PR-11 → **v0.1.0**  
**Next when resuming:** PR-2 (`tars-agent` bootstrap)

---

## First milestone (Definition of Done)

- [x] `TARS` public repo + design doc on GitHub
- [x] Pokemon cluster GitHub cleanup (early PR-10)
- [ ] PR-2 smoke test: `tars chat` text-only before skills — **deferred**
- [ ] `terminal.cwd` / `TARS_WORKSPACE` loads `AGENTS.md` — **deferred**
- [ ] `weather` skill geocodes place names via Nominatim
- [ ] `trail-search` uses `search.py` → SearXNG at `127.0.0.1:8080`
- [ ] User `SOUL.md` merged (PR-8); not Hermes default boilerplate
- [ ] PR-11 setup docs merged before PR-10 archive
- [ ] `TARS_JEEP` history purged of DB blobs before archive

---

## Open questions (remaining)

1. Benchmark tool-calling OpenRouter model before v0.2.0 (interim: `google/gemma-2-9b-it`)
2. SearXNG Docker Desktop vs WSL2 on Boot Camp
3. ATAK direct CoT vs Meshtastic-only for L5 v1
4. SOUL.md humor dial as structured frontmatter?
5. ~~TARS visibility~~ — **resolved: public**
6. ~~Git history purge~~ — **resolved: mandatory**
7. RTX Spark vs MeLE timeline

---

## Review status

All **24** review issues addressed (21 Pass-1 + 3 Pass-2: N-1 config schema, N-2 version `0.0.1`, N-3 weather diagram). See `grok-design-review-90cbc947.md` Revision Summary.
