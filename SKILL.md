---
name: build-to-learn
description: Section-by-section methodology for implementing something that doesn't exist yet — a model, a pipeline, a feature — while genuinely learning both the general concept and the particulars of whatever reference technology it's built on. Sibling to repo-deep-dive, but for the opposite starting point — repo-deep-dive is for exploring an existing unfamiliar codebase; this is for building something new, where part of the reference is Claude's own domain knowledge, not just a repo to read. Before writing any section's code or explanation into the study plan, asks the reader open questions in chat about what that section needs and why, and only writes it — with real, smoke-tested code, its actual output pasted in, never hand-computed — once the reader answers correctly, so copy-pasting without understanding isn't possible. Use when the reader says things like "quiero implementar X mientras aprendo cómo funciona", "ayúdame a construir esto entendiendo cada paso, no me des solo el código", "quiero aprender a construir un modelo/pipeline usando Y como referencia", "guíame para implementar esto sin que yo solo copie y pegue", or otherwise wants to build something new with real understanding at each step rather than finished code handed over.
---

# Build to Learn

A method for implementing something that doesn't exist yet — while genuinely learning it, not just
producing working code.

Where `repo-deep-dive` (a separate, sibling skill — not required for this one to work) starts from
an existing, unfamiliar codebase
and works toward understanding it, this skill starts from a **goal with no finished implementation
yet** — a model, a pipeline, a feature — and works toward building it, using whatever reference
material exists (a related codebase, a paper, official docs) plus general domain knowledge, while
the reader genuinely understands every conceptual step, not just the mechanics of code that happens
to run.

The core difference from just handing over working code: **before any section's content is written
down, the reader has to show they understand what that section needs and why** — in chat, through
open questions, not a self-report of "I get it." Only then does that section's goal, references,
and a real, smoke-tested snippet get written into a study-plan document.

---

## Before starting: calibrate

Ask a short, targeted set of questions about what the reader already knows, split into two axes
this skill treats separately:

1. **The general concept** being implemented (e.g. what a vision-language model is, what a
   transformer encoder does) — usually something with an existing literature and common vocabulary
   Claude already knows well from training and can supplement with a web search.
2. **The specific reference technology** the implementation is built on or informed by (e.g. one
   model's exact architecture, one library's API) — usually narrower and less documented, and the
   reader's level here can be completely different from their level on (1). Someone fluent in deep
   learning generally can be a complete novice on one specific model's internals, the same way
   someone senior in software generally can be a novice in one unfamiliar repo's domain (see
   `repo-deep-dive`'s own calibration note).

Place the reader on this 5-level scale, kept identical to `repo-deep-dive`'s so the two skills stay
consistent when used side by side on the same project:

1. Everyday language only. Vague goals. Can't evaluate an explanation beyond "that makes sense."
2. Some domain terms, possibly imprecise. Catches obvious errors in an explanation; misses
   plausible-looking wrong ones.
3. Decomposes problems. Uses general analytical language (parameterize, decompose, normalize).
   Recognizes a wrong approach but relies on the summary for the correct one.
4. Specifies what and how at a technical level. Precise domain terms. Catches non-obvious errors.
   Proposes alternatives with justification.
5. Full command of the domain. Evaluates nuanced alternatives; distinguishes better from merely
   different.

Calibrate axis (1) and axis (2) separately — a reader can sit at Level 4 on general deep learning
and Level 1 on the one architecture the project depends on. Re-check per section rather than
assuming one level covers the whole project, the same way a repo's different concerns rarely share
one level either. Treat a resume or job title as a prior, not a measurement.

**Ask how the reader best internalizes a new concept**: a precise definition, a worked example, an
analogy to something they already know, contrast with a term they'd confuse it with, or just seeing
it used in context. Use their answer for every explanation from here on, and for how you phrase the
gate questions below — a reader who learns by contrast responds better to "why not X instead of Y"
than to "explain Y."

(The level scale and the internalization-method question are adapted from the dialogic-bootstrapping
teaching methodology in [SwRI-IDEA-Lab/vocal_prompt](https://github.com/SwRI-IDEA-Lab/vocal_prompt),
the same source `repo-deep-dive` credits — reused here for consistency across both skills.)

**Ask how wide the gate should be**: every section without exception (mechanical steps included —
installing dependencies, downloading a checkpoint, setting up an environment), or only sections with
real conceptual content, with mechanical steps handed over directly. Neither is a wrong default; it
depends on whether the reader wants forced engagement even where there's no concept to test, or
would find that friction pointless. Whatever is chosen, apply it consistently through the whole
plan rather than deciding section by section on the fly.

**Confirm the output language** for `study_plan.md` and the conversation itself — don't infer it
from the request's own language alone, the same reasoning `repo-deep-dive` applies.

**Confirm sensitivity**: is the reference technology, the target codebase, or any data involved
something that shouldn't leave the reader's machine? Same handling as `repo-deep-dive` — when in
doubt, keep it local and ask before publishing or committing anything derived from it.

---

## Ground yourself before section 1

Unlike `repo-deep-dive`, there is no existing repo to survey wholesale up front — ground only what
the plan actually needs, as it comes up, rather than one big upfront pass:

- If there's a reference codebase (e.g. a paper's official implementation), read the *actual*
  source for whatever the first few sections will touch — constructors, real shapes, real config
  values — not just its README or the paper's abstract. Verify by running something real wherever
  possible (a shape, a parameter count, a real config file) rather than asserting from the paper
  alone; papers and READMEs drift from the code that actually ships.
- If there's no existing implementation at all (the reader is building something genuinely novel),
  ground the *general* concept instead — established literature, common patterns other
  implementations use for the same class of problem, a web search where training knowledge might
  be stale — and say plainly when a design choice is genuinely undecided rather than a known-good
  default, since that's a decision to make together with the reader, not a fact to state.
- Flag every inference as an inference. Never present a guess as a verified fact — same rule
  `repo-deep-dive` applies to reading an unfamiliar repo.

---

## Build the study plan document

Write a single `study_plan.md`, ordered from the most concrete grounding step (confirm real
shapes/behavior of whatever the implementation depends on) toward the most original design work
(the genuinely new pieces nobody has built exactly this way before), then to how the pieces
integrate into the whole.

### The gate, concretely

For the section currently active:

1. State the section's **goal only** — what needs to exist at the end, in one or two sentences. No
   code, no reference file names, no explanation of *how* yet.
2. Ask 1–3 open questions in chat, phrased in the reader's confirmed internalization style, that
   only someone who already understands what this section needs — and why — could answer. Prefer a
   question with real stakes over a definition-recall one: "why can't we just use X here" (where X
   is a tempting-looking shortcut that's actually wrong), "what happens to Y if we skip this",
   "what do you expect these dimensions/values to be, and why".
3. If the answer is right, or right enough to show real understanding rather than a lucky guess:
   confirm what was right, correct anything imprecise, and move to step 4. If it's wrong or shows a
   real gap: explain it using the reader's internalization method, then re-ask a related question —
   don't unlock the section on a wrong answer. Don't let this turn into an exam, either: if two
   attempts don't land, teach it directly and move on rather than making the reader feel stuck.
4. Only now write the section into `study_plan.md`: the goal, the reference material (see the two
   shapes below), and a code snippet that is **run for real, its actual output pasted in — never
   computed by hand or guessed at**. A wrong hand-guessed output teaches the wrong lesson more
   effectively than no output at all.

Every other section gets only a one-line summary until the reader is ready for it:

```markdown
## N. <topic>
<one-line summary of what this section will cover>
```

Same pacing rule as `repo-deep-dive`, same reasoning — the pacing is the point, not an inefficiency
to optimize away. Do not pre-fill several sections at once even if it would save a round-trip.

### Per-section content, once unlocked

A section is one of two shapes — or a mix of both, when that's what it actually is; don't force a
section into a shape it doesn't fit.

**Reference-grounded** (the section leans on a real, existing implementation — a library function,
a model class, an API): fill in this template. It is deliberately identical in shape to
`repo-deep-dive`'s own per-section template — copied here on purpose rather than pointed at, so
this skill works whether or not `repo-deep-dive` happens to be installed alongside it.

For each reference file that is a **module** (defines functions/classes consumed elsewhere, as
opposed to a config file, a raw data file, or a standalone script nobody imports), fill in "Where
they're used"/"Dónde se usan": search the codebase for where each function/class is actually
imported and called, and name each call site with a one-line note on what it's used *for* and
roughly *where* in that caller's flow — don't skip the search and guess. Group this by file, using
the file name in bold as a plain lead-in line, when a section has more than one reference file.
Omit the whole subsection if none of the section's reference files are modules.

For each function or method the section is actually about, fill in "What each function is
for"/"Qué resuelve cada función": a Google-style summary (purpose, `Args` with types,
`Returns`/`Raises` with types) plus **one worked example per distinct behavior described in its
purpose** — not just one example overall. **Run every example for real and paste its actual
output — never compute it by hand.** A hand-guessed "expected" output that doesn't match the real
function teaches the wrong lesson.

**When the function is an instance method** (its real signature starts with `self`), write the
worked example as if it were a free function whose first argument is an explicit stand-in for the
instance — named after what it represents (`client`, `parser`), never literally `self`, and never
using bound-method call syntax. Call it like any other positional argument: `process_batch(client,
items)`, not `client.process_batch(items)`. **Check the real signature before assuming a stand-in
is needed at all**: a `@staticmethod` never takes `self`, so define it as an ordinary module-level
function and call it by its bare name; a `@classmethod` takes `cls` and is called on the class, not
an instance — its stand-in is a class, never an instance variable. Getting this wrong implies the
method reads per-instance state that a `@staticmethod` by definition cannot have.

**Build the stand-in instance by calling the class's real constructor with plain demo values.**
Before writing that build line, actually trace what the real constructor does — read its body, not
just its signature — and list every file it reaches into as its own bullet under "Reference
files"/"Archivos de referencia", even a file that never appears in the method being documented. If
that trace turns up a constructor that resolves paths off its own module's `__file__` (e.g.
`Path(__file__).resolve().parents[N]`), running it unmodified in a notebook raises `NameError` —
shim it instead, with a comment explaining why:
`__file__ = str(Path.cwd() / "<matching/relative/path.py>")`.

**Every worked example calls the function on a named fixture from that section's supporting
material, never an unlabeled inline literal** — the reader needs to run the *identical* call
against their *own* implementation and check it produces the *identical* output, which only works
if they can see exactly which fixture feeds the call. If truly no fixture fits, a literal is
acceptable, but say so — that isn't the common case.

Close each function's block with "Defined in"/"Se define en" naming the single reference file the
function lives in (required whenever a section lists more than one reference file), followed by
"Used in"/"Se usa en" listing just the file names that call *this specific* function.

**Every file reference is a clickable relative link, not a plain code span** —
`` [`<file>`](<relative-path>) `` — computed from `study_plan.md`'s own location, verified to
resolve (e.g. `ls` the computed path) before writing it.

```markdown
## N. <topic>

### Reference files

- [`<file>`](<relative-path>) - <one line on what it demonstrates>

### Where they're used

(omit this subsection if no reference file above is a module)

**[`<file>`](<relative-path>)**
1. [`<caller file>`](<relative-path>) - uses it for <what> in <where in that file's flow>

### What each function is for

#### a) `function_name(arg1, arg2)`

**Purpose:** <what problem this function solves, in one or two sentences>.

- `arg1` (`<type>`): <what it is>
- `arg2` (`<type>`, default `<value>`): <what it is>

Returns `<type>`: <what comes back, including edge cases like None/empty>.

```python
function_name(<real example input>)
```
→ `<the real, executed output>`

Defined in: [`<file>`](<relative-path>).

Used in: [`<file>`](<relative-path>).

### Proposed notebook name

`0N-<slug>.ipynb`

### Supporting material

- [`<support file prepared for this section>`](<relative-path>) - <what it exemplifies>
```

(Spanish variant: `### Archivos de referencia`, `### Dónde se usan`, `### Qué resuelve cada
función`, `**Propósito:**`, `Devuelve`, `Se define en:`, `Se usa en:`, `### Propuesta de nombre del
notebook`, `### Material de apoyo` — same content and shape, headers only in the language confirmed
during calibration. Never mix the two languages within one document.)

**Original design** (the section has no existing implementation to point to — a genuinely new piece
being designed for this project, like a novel projector layer or a training loop): instead of
reference files, write a short design-rationale block:

```markdown
### Design rationale

**Qué se decidió:** <the choice, in one line>.

**Alternativas consideradas:**
- <alternative> — <why it was set aside>
- <alternative> — <why it was set aside>

**Por qué esta:** <the reasoning, grounded in the concept and, where it exists, in literature or
established practice for this class of problem — cite what informed it>.

**Juicio, no hecho establecido:** <say plainly if this is a judgment call rather than a known-good
default, and what would change the decision>.
```

Then the real, smoke-tested implementation that resulted — same standard as any other snippet in
this plan.

**Once the reader confirms a section's notebook is actually finished**, retire that section's
forward-looking `### Proposed notebook name`/`### Propuesta de nombre del notebook` subsection
entirely, and add a `### Development notebook`/`### Notebook de desarrollo` subsection in its
place — moved to the very *top* of the section's block, right after its `## N. <topic>` heading and
before `### Reference files`/`### Archivos de referencia` (or before `### Design rationale` for an
original-design section). It holds a clickable relative link to the real notebook file the reader
wrote:

```markdown
### Development notebook

[`01-normalization.ipynb`](../<replica-or-project>/notebooks/01-normalization.ipynb)
```

The real filename may differ from the proposed slug — use whatever the reader actually named it.
This turns each finished section's block from a forward-looking checklist into a running index of
what was actually built, with a working link straight to it, visible before anything else in that
section.

### Track design decisions as they surface

Studying a reference closely enough to write a notebook about it, or designing an original piece
from scratch, surfaces things the upfront grounding pass never catches — often only found once
deep enough in one piece to try a real alternative (e.g. discovering an established pattern handles
a case a first design missed, and proving it with a real comparison rather than asserting it).
Capture these in a second living document, `design_decisions.md`, in the same directory as
`study_plan.md`, once a few "original design" sections exist — accumulated gradually, only as real
findings surface, not pre-populated for sections not yet reached.

Structure it with one `##` heading per `study_plan.md` topic, using the exact same numbers and
titles, so the two documents cross-reference cleanly:

```markdown
## N. <topic, matching study_plan.md exactly>

### <short name for the decision>

Qué es: <one or two sentences>.

A favor:
- <concrete advantage>

En contra:
- <concrete tradeoff or cost>

Evidencia: <the real comparison/demo that supports this — never a claim without one; link or
reproduce the actual test run>.
```

For each entry, give the reader real decision-support, not a unilateral recommendation — this
document exists so they can bring it to whoever else has a stake in the project and discuss it, not
so Claude decides for them alone. When an entry proposes swapping in a library or a new dependency,
don't leave "adds a dependency" as a vague con — measure it (installed size, a real runtime
benchmark comparing old and new on both the rare case and the common one) rather than asserting it.
This is often exactly the material a later model-card / architecture-decisions writeup needs, so
keeping it as you go is cheaper than reconstructing it afterward from memory.

### What never belongs in the plan

- A code snippet that was never actually run — hand-computed or guessed output is worse than no
  output, because it looks verified when it isn't.
- A design-rationale block presented as settled fact when it was actually a judgment call — say so
  explicitly (see "Juicio, no hecho establecido" above), so the reader can revisit it later with
  real information instead of trusting a guess that was dressed up as a decision.
- Real credentials, internal URLs, or private data copied into the plan or its supporting material,
  even when the reference codebase has them — same rule `repo-deep-dive` applies to its replica.

---

## Hard rule for this skill file itself

This file is meant to be reused across many different, unrelated projects. When updating it after
using it somewhere, genericize any lesson learned before it lands here — never let a specific
project's real names, business details, technology choices, people, internal tools, or findings
leak into this file. This applies to every part of an edit — the prose, the code identifiers, the
sample values in an example, all of it — not just the explicit claims. Before considering an edit to
this file done, reread the exact text you're about to write (or grep it) for any term specific to
the project you were just working in — a function name, a domain concept, a sample value — and
replace it with a generic placeholder if found. Writing the lesson in generic terms from the start
is easier than sanitizing it after; don't draft it against the real names and plan to clean up later.
