# Contributing to storm-skill

Thanks for your interest in improving `storm-skill`. This is a small project — a
Claude Agent Skill made of Markdown instructions, reference docs, and one
standard-library Python helper — so contributing is lightweight. The most useful
contributions are improvements to how the skill *behaves*: better perspective
discovery, stronger source grounding, clearer instructions, and bug fixes in the
helper script.

## Ways to contribute

- **Report a bug or rough edge** — open an issue describing what you ran, what the
  skill produced, and what you expected. Concrete examples (the topic you used, the
  output you got) are far more useful than abstract descriptions.
- **Improve the skill** — tighten `storm/SKILL.md`, the reference files, or the
  `storm_run.py` helper. See "Project layout" below.
- **Suggest an idea** — open an issue before a large change so we can agree on the
  approach first.

## Project layout

```text
storm/
├── SKILL.md                 # the orchestrator: the 6-stage pipeline
├── references/
│   ├── method.md            # mapping to the STORM / Co-STORM papers
│   ├── interviewer.md       # brief handed to each interview subagent
│   └── report-template.md   # report structure, citation + reliability rules
└── scripts/
    └── storm_run.py         # run scaffolding + deterministic source merging
```

If you change the pipeline in `SKILL.md`, check whether the reference files or the
helper need to change to match — they're meant to stay in sync.

## Guiding principles (please preserve these)

- **Retrieval grounding is the point.** Every expert answer and every claim in the
  output must trace to a real retrieved source. Don't add steps that let the skill
  answer from memory — that's the failure mode this project exists to avoid.
- **Perspectives are discovered, not hardcoded.** Keep the "survey first, then
  derive perspectives" approach rather than baking in a fixed cast.
- **Faithful to the method.** This re-implements Stanford STORM's approach; if you
  extend it, keep `references/method.md` honest about what maps to the papers and
  what's new here. See [NOTICE](NOTICE) for attribution.
- **Keep the helper dependency-free.** `storm_run.py` uses only the Python standard
  library. Please don't add third-party dependencies to it.

## Changes to the helper script

- Target Python 3.8+ and standard library only.
- `storm_run.py` is meant to be deterministic and safe to re-run; preserve that
  (for example, source numbering should stay stable, and runs should stay inside
  the `storm-runs/` directory).
- If you change its behavior, include a quick before/after example in your PR so
  reviewers can see the effect.

## Submitting a change

1. Fork the repo and create a branch for your change.
2. Keep pull requests focused — one logical change per PR is easier to review.
3. Describe what you changed and why. If it changes skill behavior, show a sample
   run or output snippet.
4. By contributing, you agree your contributions are licensed under the project's
   [MIT License](LICENSE).

## Testing your change

There's no formal test suite. Before opening a PR, sanity-check that:

- `python3 storm/scripts/storm_run.py init "some topic"` scaffolds a run, and
  `merge` produces a numbered `sources.md`.
- If you changed the pipeline, run the skill end-to-end on a real topic in Claude
  Code and confirm the report stays grounded (every `[n]` maps to a real source).

## Code of conduct

Be respectful and constructive. Assume good faith, keep feedback about the work,
and help keep this a welcoming place to collaborate.
