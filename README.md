# build-to-learn

A Claude Code skill for implementing something that doesn't exist yet — a model, a pipeline, a
feature — while genuinely learning it, not just getting working code out of the session.

Sibling to [`repo-deep-dive`](../repo-deep-dive/README.md), but for the opposite starting point:
`repo-deep-dive` explores an existing unfamiliar codebase; `build-to-learn` builds something new,
using a reference implementation, a paper, or general domain knowledge as the material — with
Claude's own knowledge and web access standing in for "a repo to read" when no existing
implementation exists yet.

The core mechanic: before any section's code or explanation is written into the study plan, Claude
asks the reader open questions in chat about what that section needs and why. Only once the reader
answers correctly does the section get written — with a real, smoke-tested snippet, never
hand-computed output.

See [SKILL.md](SKILL.md) for the full methodology.

## Install

Clone this repo into your Claude Code skills directory:

```bash
git clone <repo-url> ~/.claude/skills/build-to-learn
```

Claude Code picks up any skill under `~/.claude/skills/<name>/SKILL.md` automatically — no further
setup needed.

## Use

In a Claude Code session, working toward implementing something new:

```
/build-to-learn
```

or just describe what you want in your own words (e.g. "quiero implementar un X mientras aprendo
cómo funciona, no me des solo el código") — the skill's description covers those trigger phrases
too.

## Credits

The reader-level scale and the "how do you best internalize a new concept" calibration question are
adapted from the dialogic-bootstrapping teaching methodology in
[SwRI-IDEA-Lab/vocal_prompt](https://github.com/SwRI-IDEA-Lab/vocal_prompt) — the same source
`repo-deep-dive` credits, reused here for consistency across both skills.
