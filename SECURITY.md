# Security Policy

`storm-skill` is a Claude Agent Skill: Markdown instructions, reference docs, and
a small Python helper (`storm/scripts/storm_run.py`) that uses only the standard
library. It ships no service, no released binaries, and no runtime that ingests
untrusted network input. The realistic security surface is therefore small, but a
few things are still worth taking seriously.

## What counts as a security issue here

- A flaw in `storm_run.py` that could write outside the intended `storm-runs/`
  directory, mishandle a crafted topic string, or otherwise behave unsafely on
  attacker-influenced input.
- Skill instructions in `SKILL.md` or the reference files that could be abused to
  make an agent take an unintended action (for example, prompt-injection paths
  introduced by the skill itself).
- Any secret, token, or credential accidentally committed to this repository.

Note that this skill instructs an AI agent to run live web searches and read web
pages. Content retrieved from the open web is untrusted by nature; treat anything
the skill surfaces from a source as data, not as instructions, and review
side-effectful actions before running them. That is an inherent property of
research-on-the-web, not a vulnerability in this repo.

## Reporting

Please report suspected vulnerabilities privately rather than opening a public
issue. Use GitHub's private vulnerability reporting (the **Report a vulnerability**
button under this repository's **Security** tab).

Include enough detail to reproduce: what you did, what happened, and what you
expected. A minimal example or proof of concept helps.

## What to expect

This is a small, community-maintained project, so responses are best-effort. I aim
to acknowledge a report within about a week, confirm whether it's in scope, and —
if it is — fix it in a reasonable timeframe and credit you in the commit or release
notes unless you'd prefer to remain anonymous.

## Out of scope

- Vulnerabilities in third-party services the skill talks to (Claude, search
  providers, the websites it retrieves) — report those to the relevant vendor.
- Issues that require an already-compromised machine or a malicious local user.
- The general fact that an LLM can produce inaccurate output; please report
  correctness problems as normal issues, not security reports.

## Supported versions

This project is distributed from the `main` branch and has no formal release
cadence. Fixes land on `main`; please track the latest commit.
