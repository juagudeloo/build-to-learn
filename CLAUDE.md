# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this
repository.

## What this repository is

This is a single Claude Code **skill package** (`build-to-learn`), not an application. There is no
build, lint, or test tooling — the repository consists of `SKILL.md` (the methodology Claude
follows when the skill is invoked) and `README.md` (install/usage instructions for humans). There
is no other code in this repo.

The skill is installed by cloning this repo into `~/.claude/skills/build-to-learn`, where Claude
Code auto-discovers it via `SKILL.md`. There is no packaging or publish step beyond committing
changes to this repo.

## Sibling to repo-deep-dive

`build-to-learn` was split out of `repo-deep-dive` deliberately, not merged into it: `repo-deep-dive`
starts from an existing unfamiliar codebase; `build-to-learn` starts from a goal with no
implementation yet. They share the calibration block (5-level scale, internalization-method
question, both credited to [SwRI-IDEA-Lab/vocal_prompt](https://github.com/SwRI-IDEA-Lab/vocal_prompt))
and the per-section reference-file template almost verbatim — this is intentional duplication, not
an oversight, since skills are meant to be self-contained rather than importing from one another at
runtime. When one skill's shared block improves, consider whether the other should pick up the same
improvement, but don't force the two files to merge.

## Working on this repo means editing `SKILL.md`

Any task here is almost always "improve the methodology in `SKILL.md`." Treat `SKILL.md` as the
deliverable, not as documentation of separate code. Read it in full before editing.

## The hard rule (from `SKILL.md` itself)

`SKILL.md` explicitly states, at its end, that it must stay generic:

> This file is meant to be reused across many different, unrelated projects. When updating it after
> using it somewhere, genericize any lesson learned before it lands here — never let a specific
> project's real names, business details, technology choices, people, internal tools, or findings
> leak into this file.

When asked to fold a lesson learned from using this skill on some other project back into this repo,
strip out anything specific to that project (names, stacks, org details) before writing it into
`SKILL.md`. This rule applies with equal force to `README.md` and to this `CLAUDE.md` file.

## Structural conventions to preserve when editing `SKILL.md`

- **Two-axis calibration**: general concept vs. specific reference technology are calibrated
  separately, since a reader's level on one says nothing about their level on the other.
- **The gate is the point**: no section's code or explanation is written into the plan before the
  reader answers open questions about what it needs and why. This is the feature that most needs
  protecting from erosion — don't let an edit quietly turn it into "ask if they want to try it
  first" (a weaker, binary version of the same idea that already exists elsewhere as a fallback
  default, not as this skill's actual mechanism).
- **Two section shapes**: reference-grounded (points at real, existing code) and original-design
  (a design-rationale block, since there's nothing existing to point at) — keep both, since forcing
  every section into the reference-file template breaks for genuinely new work.
- **Smoke-tested code only**: every snippet that lands in the plan must have actually been run, with
  its real output pasted in. A hand-computed or guessed output is explicitly called out as worse
  than none at all — preserve that framing, don't soften it to "try to verify when possible."
- **Incremental disclosure**: only the active section gets the full template; every other section
  gets a one-line summary. This pacing is intentional, not an inefficiency to fix.
