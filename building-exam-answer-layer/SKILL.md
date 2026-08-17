---
name: building-exam-answer-layer
description: Use when a student has a finished HTML study page and now needs to rehearse writing answers under exam time pressure rather than re-read them — adds a compact, writable "exam answer" above every question with the full answer collapsed beneath, plus a trigger sheet mapping question phrasing to the framework it wants. Triggers include "I can't write this fast enough", "make a compact answer version", "what do I actually write in the exam", "how do I know which framework the question wants", "trigger sheet", "I only have 6 minutes per question", "too many questions, not enough time".
---

# Building Exam Answer Layer

> **Start with `exam-prep-intake`** if the scope is not already settled. It asks one round of questions (what to build, what the exam is like, answer length, cross-topic links), derives the professor's answer shape, and hands over. Skip it only when those answers are already in hand.

## Overview

A finished study page tells the student **what is true**. It does not tell them **what to write in six minutes**.

This skill adds two things on top of an existing page (normally a recap page, but a full reference page works too):

1. **A compact `⚡ Exam answer` band at the top of every question and every worked exercise** — telegraphic, keyword-dense, sized to the real clock, with the example kept.
2. **A `⚡ Trigger sheet` at the top of the file** — how a question is phrased on the left, which framework to reach for on the right.

The existing answer is not deleted. It moves into a collapsed `▸ the long version, for learning` underneath. The page becomes **two-speed**: learn from the long version once, then only ever re-read the compact one.

This is a downstream skill. It edits a page that already exists and is already trusted.

## When this skill is the right one

It is triggered by a **time** problem, not a knowledge problem. The signals:

- The student says some version of *"I know this, I just can't write it fast enough."*
- The exam has many questions worth few points each.
- They are anxious about **recognising** which framework a question wants, not about the frameworks themselves.

If they still do not understand the content, they need `building-exam-reference-html`. If they want to re-read faster, they need `building-exam-recap-html`. Only when both of those are done does this one pay off.

## Core principle

**Two speeds in one file, and the compact version is always derived from the long one.**

Never write a fresh, thinner answer. Compress the answer that is already on the page. A separately authored short answer drifts from the long one, and the student ends up unsure which to trust, which destroys the value of both.

The reason the layer works: **recognition is fast, reconstruction is what eats the clock.** The depth already on the page is not wasted; it is what makes the compact version feel like transcription instead of thinking.

## Workflow

### 1. Get the exam's real logistics first. Do not skip this.

If `exam-prep-intake` ran, you already have these and must not re-ask. Otherwise, ask for or find:

- **How many questions**, and how many bundles or parts.
- **How long** the exam is.
- **How the marks are distributed** — same per question, or heavier on some.
- **How many pages** of answer space, if the paper is structured.
- **The pass rate**, if they know it.

Then do the arithmetic out loud and give it back to them:

```
28 questions ÷ 180 minutes  →  ~6 minutes each
minus ~15 min reading and checking  →  under 6
24 pages ÷ 28 questions  →  well under a page per answer
```

**That number is the specification.** Six minutes means 8 to 12 lines, in bullets and keywords. It rules out the essay the page currently implies, and it tells you how long each compact band may be.

It also reframes the student's fear, which is usually worth as much as the artifact. A 75% failure rate on a paper with this ratio is rarely people who did not know the material; it is people who wrote three beautiful answers and left ten blank.

### 1b. Derive the answer shape from this professor, do not import one

A compact answer is only compact in the right *order*. That order comes from the lecturer, and it is not transferable.

- Collect their **question verbs** from review slides, sample questions and past papers. *"In your own words explain"*, *"how is it constructed"*, *"why is it important"*, *"suppose"*, *"give a concrete example"*, *"what are the risks"* dictates a specific band order: define → parts → why → apply → example → risk. A different lecturer's verbs dictate a different one.
- Check whether the course **publishes named question styles**, for example *reproduce / relate / translate to an example / apply the technique*. If it does, tag every band with which style it is, because each wants a different answer: a named list, a two-column contrast plus the consequence, one concrete instance, or the working shown line by line.
- Treat any **published model answer as the marking structure**. If the official solution is laid out in three numbered steps, three numbered steps is the format — that is not a study trick, it is the grader's own shape.

**If one paper covers two lecturers, build two shapes.** Carrying one professor's structure into another's topic is a quiet, systematic way to lose marks across a whole topic.

### 1c. Give them an order to answer in, not just a budget

Step 1 tells the student how many minutes each question is worth. It does not tell them **which question to write first**, and on a paper with more questions than time that is the decision that actually sets the mark. The documented failure is not ignorance, it is three beautiful answers and ten blanks.

So put a **triage protocol** in the trigger sheet of every page you build:

> **The first minutes are not writing minutes.** Read the whole paper, label every question, then answer in label order. Budget about 5 minutes, or 8 to 10 if the paper is long.

Label each question on two axes the student can judge at reading time:

- **Payoff** → how many marks it carries
- **Ease** → how fast and confidently *this student* can write it

|  | Easy for me | Hard for me |
|---|---|---|
| **High marks** | **I** · do **first** | **C** · do **third**, with a time cap |
| **Low marks** | **P** · do **second**, cheap and fast | **K** · do **last**, but never blank |

Two rules that matter more than the grid:

- **Nothing is ever abandoned.** If the course this comes from calls the last quadrant "kill", say explicitly that an exam is the one place that word does not apply: a blank scores zero for certain, a two-minute skeleton of named terms scores something. The last quadrant means *last*, not *skipped*.
- **The order is a default, not a law.** It is really *marks per minute*. If one hard question carries a large share of the paper, cap the easy low-mark ones and get to it while there is still thinking time left.

**Prefer a framework the student already knows.** If their course taught a prioritisation grid — a PICK chart, an effort-impact matrix, a payoff matrix — reuse its letters and axes rather than inventing a scheme. They will already be able to draw it from memory under pressure, which is the whole point, and it costs zero extra revision. Say which course and lecture it came from so the reuse is visible.

Note the symmetry worth pointing out to them: `building-exam-recap-html` ranks *sections* into tiers for study time; this ranks *questions* into tiers for exam time. Same move, two different rooms.

### 2. Agree the shape on one question before building at scale

Mock up a single question with both layers and show it. A topic can easily have 40 to 60 questions, and rebuilding them all because the band was too long, too terse, or wrongly stamped is the most expensive mistake available here.

Settle explicitly: does the long version collapse or stay open; which topic gets built first; whether the trigger sheet comes in the same round. Then build.

### 3. Derive each compact answer from the long one

Read the existing answer. Keep, in this order of priority:

1. **The framework's own named parts**, in the course's exact words. This is what the grader scans for.
2. **The example.** In an exam graded against model answers a missing example loses its own mark. Shorten it; never drop it.
3. **The trade-off, limitation, or trap.** The half most students skip, and therefore cheap marks.
4. **The one-line "what the marks are actually for"** note, if the page has one.

Cut: build-up sentences, an idea phrased twice, the paragraph wrapped around an anecdote, and any hedging.

### 4. Write it telegraphically, in aligned columns

The compact band is not prose. It is what a hand writes under pressure.

- **Bold the terms the grader is scanning for**, and nothing else.
- Use structural markers: `①②③`, `→`, `·`, and short ALL-CAPS labels (`DEF`, `EX`, `WHY`, `TRAP`).
- **Align comparisons into columns.** A two-column contrast is faster to read and faster to copy than the same content as sentences.
- Abbreviate the way a student under time pressure abbreviates.
- Keep formulas, tables of solved numbers and drawn diagrams **at full size**. They are already minimal, and each row is usually its own gradable point.

### 5. Stamp every band with a time estimate and what is graded

`⚡ Exam answer · ~6 min · 3 values + 4 indicators + interpret + act`

**Size the estimate per question by counting the graded elements**, never uniformly. A definition question is 3 minutes; a draw-plus-apply question is 10. Tell the student explicitly that these are your estimates from counting graded parts, not the professor's mark scheme.

**Deliberately over-provision, and say so.** Put the framework's own words at the top of each band and the polish at the bottom, so that stopping two thirds of the way down still leaves a scoring answer. It is far better to give the student something to cut than to have them run out of material.

If the totals across all bands exceed the exam's total minutes, that is expected and worth reporting. It tells the student the bands are a ceiling, not a target.

### 6. Preserve the long version, collapsed

Wrap the original content in a nested collapsible labelled **`▸ the long version, for learning`**. Nothing is deleted. The student uses it to understand a question the first time and never opens it again.

Collapsing rather than leaving it open is the right default: on a fast-review pass, an open long answer means scrolling past hundreds of lines to reach the next question.

### 7. Build the trigger sheet

A collapsed block at the very top of the file. Three columns: **how a question is phrased · what to reach for · a link to the full question.**

- **Phrase the left column the way an exam paper actually phrases it**, in quotation marks, including the vague versions: *"why does this keep going wrong"*, *"which one would you tackle first"*, *"is this redesign any good"*.
- The right column is the framework **plus its trigger detail** — the formula, the named parts, the one move that scores. Not a definition; the student already knows the definition.
- Link each row to the question, and make the link **open the collapsed answer**, not just scroll to a closed box.

Then say the honest thing in the sheet itself: **you rarely have to detect a framework from nothing.** Most questions name the tool, or the module makes it obvious. The sheet is for the two or three that do not. Saying this removes more anxiety than the sheet does.

Close the sheet with the moves that work on every question (name the framework in the course's words · apply it with the case's own nouns · always give an example · state the trade-off), the timing rule from step 1, and the **triage protocol from step 1c** — the label-then-answer order belongs at the top of the sheet, because it is the first thing the student does on the day and the only part they use before writing a single word.

### 8. Adapt the emphasis to each topic's mark structure

If one half of the paper has more questions worth fewer points each, say so in that file's trigger sheet and make its bands shorter. **Breadth beats depth where marks are thin**; depth pays where a single question is worth a lot. The two halves of a paper often deserve different advice, and giving both the same advice wastes the difference.

### 9. Audit

Beyond the usual tag balance and link resolution:

- **Collapsible depth is now 2, not 1.** Assert it is exactly 2 and returns to 0. A duplicated opening tag here silently swallows the rest of the page.
- **No horizontal scroll.** Measure the longest line in every compact band and keep it under the container width (about 68 characters for a monospace block). Wrapping is fine; a sideways scrollbar in a band the student is trying to read at speed is not.
- **Every question has exactly one band**, and running the build twice does not double them.
- **Report the totals**: bands built, time-chip sum, longest line.

## Implementation notes

**Insert, never re-render.** These pages are usually hand-edited by the student. Work by depth-aware string surgery on the existing file: find the answer container's opening tag, walk forward counting opens and closes to find its true match, insert the band before the original content and wrap that content in the collapsible. Assert the marker occurs exactly once before every replacement, and assert the band is not already present so a re-run is a no-op.

**Give the band its own colour token**, distinct from every callout type already on the page, so the eye finds it instantly. A green reading as "go, write this" works well against the usual red-trap and amber-warning palette.

**Use `white-space: pre-wrap`, not `pre`.** It preserves the column alignment you wrote while letting a long line wrap instead of producing a scrollbar.

**Make links to collapsed answers actually open them.** A few lines are enough:

```js
(function(){
  function openTarget(){
    var h=location.hash;if(!h||h.length<2)return;
    var el=document.getElementById(h.slice(1));if(!el)return;
    if(el.tagName==='DETAILS'){el.open=true;el.scrollIntoView({block:'start'});}
  }
  window.addEventListener('hashchange',openTarget);
  openTarget();
})();
```

**Do the practical sessions too.** Worked exercises need this as much as theory questions, and they compress differently: lead with the method and the numbers, keep both passes of a calculation, keep the solved table, and keep the one sentence that explains the result. The teaching lines that carry marks survive verbatim.

## Common mistakes

- **Writing a fresh short answer instead of compressing the existing one.** The two versions disagree in small ways and the student stops trusting both.
- **Dropping the example to save room.** It has its own mark. Shorten it.
- **Uniform time estimates.** They are the specification for how long each band may be, so a flat number makes every band the wrong length.
- **Prose in the compact band.** If it reads like sentences, it is not compact, it is just shorter. Columns, markers, bold terms.
- **A trigger sheet that is really a glossary.** The left column must be *phrasings*, not concept names. If the student already knows the concept is called "root-cause analysis", they did not need the sheet.
- **Under-provisioning the band.** Cutting to exactly the time estimate leaves nothing to drop when the clock is against them. Give them material to cut, ordered so the cut comes from the bottom.
- **Building all 50 before showing one.** Agree the shape first.
- **Forgetting the depth-2 audit.** Nesting a collapsible inside a collapsible is where this skill breaks pages.
- **Skipping the logistics step and guessing.** Without minutes-per-question there is no principled length, and the whole layer becomes another opinion about how much to write.
- **Giving a per-question budget but no answering order.** On a paper with more questions than time, the order decides the mark. A budget alone lets the student spend it in the worst possible sequence.
- **Inventing a triage scheme when the course already taught one.** A grid the student can draw from memory beats a better grid they have to learn the week of the exam.
- **Letting "kill" mean "leave blank".** Borrowed prioritisation frameworks discard the bottom quadrant. An exam never does. Rename it out loud, or the student will follow the framework off a cliff.
