# STORM skill for Claude

A native [Claude](https://claude.ai) skill that runs deep, citation-grounded
research using the method behind Stanford OVAL's
**[STORM](https://github.com/stanford-oval/storm)** — without the Python engine.
It reproduces STORM's *way of working* (discover real perspectives → interview
each one grounded in live web search → map contradictions → write a sourced,
peer-reviewed briefing) directly inside Claude's agent loop.

> Inspired by, and not affiliated with, Stanford OVAL. STORM is MIT-licensed;
> papers and code are linked below. This re-implements the method, not the
> codebase.

## Why this exists

Asking a model to "tell me about X" gives you the majority view from memory.
STORM's insight is that good research comes from asking good questions across
several genuine perspectives, with **every answer grounded in real sources**.
This skill keeps that grounding at the center — the thing most "STORM in 4
prompts" shortcuts quietly throw away.

## What you get

Run it on a topic and it produces, in `storm-runs/<slug>/`:

- `perspectives.md` — the angles, discovered from real coverage
- `raw/*.notes.md` + `raw/*.sources.tsv` — per-perspective grounded interviews
- `sources.md` — one deduped, numbered source list (the citation keys)
- `contradictions.md` — where perspectives clash, agree, and leave gaps
- `outline.md`
- `report.md` — the briefing, with inline `[n]` citations and a reliability block

## Install

### Claude Code

Copy the `storm/` folder into a skills directory:

```bash
# project-level (this project only)
mkdir -p .claude/skills && cp -r storm .claude/skills/storm

# or personal (all your projects)
mkdir -p ~/.claude/skills && cp -r storm ~/.claude/skills/storm
```

### Claude apps / Cowork

Install the packaged `storm.skill` file from the Skills settings (Settings →
Capabilities → Skills), or upload it wherever skills are accepted.

## Use

Just ask, in plain language — you don't need to say "STORM":

> Research the current state of solid-state batteries for EVs and write me a
> sourced briefing.

> I have an investor meeting Tuesday — get me up to speed on all sides of the
> lab-grown meat market.

The skill triggers on research / deep-dive / briefing-style requests and skips
simple one-fact lookups.

## How it works

1. **Survey & discover perspectives** — broad searches, then derive 3–6 distinct
   lenses from what coverage actually shows.
2. **Grounded interviews** — each perspective is interviewed over several turns;
   answers come only from live web search, sources logged. In Claude Code these
   run in parallel as subagents.
3. **Merge + contradiction map** — dedupe/number sources, then map clashes,
   agreement, and blind spots.
4. **Outline → grounded draft** — section by section, every claim cited.
5. **Peer review** — honest self-check against the sources, with a reliability
   block surfaced at the top.

See [`storm/references/method.md`](storm/references/method.md) for the full
mapping to the STORM and Co-STORM papers.

## When to use the real engine instead

For the fully validated pipeline, reproducible benchmarks, or the interactive
Co-STORM roundtable, use Stanford's package directly: `pip install
knowledge-storm`. This skill trades that machinery for zero setup, speed, and
Claude's own retrieval.

## Credits

- STORM — Shao et al., NAACL 2024 — https://arxiv.org/abs/2402.14207
- Co-STORM — Jiang et al., EMNLP 2024 — https://arxiv.org/abs/2408.15232
- Code — https://github.com/stanford-oval/storm

## License

MIT — see [LICENSE](LICENSE). Attribution to the original STORM project is in
[NOTICE](NOTICE).
