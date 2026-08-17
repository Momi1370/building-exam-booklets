---
name: building-exam-recap-html
description: Use when a student already has a full HTML reference page (from building-exam-reference-html) and wants a much shorter re-read version of it — a fast-recap page per module plus a merged all-modules page — for the last passes before a closed-book exam. Triggers include "make a shorter version", "I want to recap fast", "condense the HTML", "one page I can re-read the night before", "merge the modules into one recap".
---

# Building Exam Recap HTML

> **Start with `exam-prep-intake`** if the scope is not already settled. It asks one round of questions (what to build, what the exam is like, answer length, cross-topic links), derives the professor's answer shape, and hands over. Skip it only when those answers are already in hand.

## Overview

Turn a finished full reference page into a **fast-recap layer**: one condensed page per module, plus a merged all-modules page. The full page is where you *learn* a topic; the recap is where you *re-read* it — on the fifth pass, the morning of the exam, on a phone.

This is a downstream skill. It does not replace `building-exam-reference-html`; it compresses its output. Downstream of *this* skill sits `building-exam-answer-layer`, which turns a finished recap into writing practice.

## Core principle

**Compaction is subtraction of prose, never of gradable content.** Every concept, every named list, every example the grader could ask for survives. What goes is the connective tissue: the build-up sentences, the second phrasing of an idea already stated, the paragraph around an anecdote. If removing something would cost a mark, it stays at full size — even if that leaves one module far less compressed than the others.

## Workflow

1. **Derive from the full page, not from the booklet.** Re-compacting from the original source re-does the interpretation work and silently drifts from the page the student already trusts. Open the full page, and compress *it*. The section list of the recap must end up identical to the section list of the full page.
2. **Build it as fragments plus an assembler**, not as N hand-written files. One content fragment per module; one small script holding the shared CSS, the page shell, and the merge. This is what makes the standalone files and the merged file byte-identical in content instead of slowly diverging. The assembler should strip the module banner from standalone builds (their page header already names the module) and keep it in the merged build (where it separates modules).
3. **Open every module with a "spine"** — one line per numbered subsection, stating that section's single load-bearing claim. This is the actual recap: the student reads eight lines and only drops into a section when a line fails to fire. Everything else on the page is there to be *skipped*.
4. **Convert prose to term → gloss rows.** Any list where each item needs a sentence of explanation becomes a two-column row — bold term, one-line gloss. Characteristics, constraints, criteria, phases, framework components. This is the single biggest space win and it reads faster than the prose did.
5. **Compress anecdotes to their trigger phrase.** The professor's stories are memory anchors and must survive, but they survive as a clause, not a paragraph — "nine women / one baby", "New Coke: feasible, desirable, not viable", "970 files, finished two weeks early". One line, keeping the punchline that makes it stick.
6. **Collapse practice questions to one-line answer skeletons** — the moves, arrow-separated, with the structural verbs bolded. Enough to rehearse the shape of an answer without re-reading a model answer the student has already absorbed. **If the student's problem turns out to be writing speed rather than reading speed** — many questions, few minutes each, "I know it, I just can't write it fast enough" — stop here and use `building-exam-answer-layer` instead, which keeps the full answer and adds a compact writable one above it.
7. **Keep tables at full size.** Comparison tables, formula tables, solved-exercise tables. They are already the fastest thing on the page to read, and in this kind of exam each row is typically a separately gradable point. Cutting rows buys almost no reading time and costs marks.
8. **Use a denser typography than the full page** — sans-serif, tighter leading, smaller margins, hairline separators. The recap should *look* like a different mode, so the student knows which pass they are on. **Denser means tighter, not narrower: inherit the full page's container width (`max-width: ~1240px`) rather than shrinking the column.** The whole point of the recap is scanning speed, and a narrow column costs lines and forces zooming on a laptop. Since `max-width` is only a ceiling, the phone layout is unaffected either way. Keep the same colour-coded callout taxonomy so the flags (exam traps, confirmed-question markers) stay recognisable across both versions.
9. **Rank what you could not shorten.** Some topics stay long because their sources are long, and a student staring at eight dense sections for a topic worth one exam question will not know where to start. The fix is **not** cutting: it is a **triage block at the top** with three tiers — *write cold*, *recognise*, *read once and skip on the last pass* — each listing its sections and carrying a minute budget. Say plainly which tier answers the likely question, and say that the bottom tier exists only so the top tier makes sense. Rank by confirmed past questions first, then whatever the booklet flags as critical.
10. **Link the topics, if the student wants it.** Two things, and they are cheap next to their value: a short per-section strip naming what the same idea is called in other topics, and one shared table of **terms that mean different things in different topics**. Reuse across the whole family reveals these fast — the same word carrying two technical meanings in two topics is a silent mark loss, because the wrong sentence still reads fluently. Put the shared table in every topic file, so the student meets it wherever they open.
11. **Audit, and report the right numbers.** Diff the recap's section list against the full page's — they must match exactly, in order. Check tags balance and internal links resolve in every file including the merge. Write the audit as a **script you re-run per topic**, not an eyeball pass: it should check tag balance, collapsible depth, link resolution, section-number sequence, and stray closing tags inside label spans. A real script catches real bugs; a careful read does not.
    - **Report a compression ratio only for a pure recap.** If you have merged `building-exam-answer-layer` into the same file, the result is *larger* than the page it came from — it carries a compact answer, the full answer, and the drills. Quoting a ratio there is actively misleading. Report band count, word count, section count and audit results instead.

## Common mistakes

- **Cutting table rows to hit a length target.** The most expensive possible saving — pure marks lost for almost no time gained.
- **Compressing every module by the same amount.** Modules are not equally compressible. A module that is mostly worked calculations and fixed step-lists may only come down by a quarter; a module that is mostly explanation may halve. Forcing a uniform ratio means over-cutting the dense one.
- **Rebuilding from the booklet instead of the full page.** Produces a recap that disagrees with the page in small ways — different examples, different emphasis — which destroys the student's trust in both.
- **Hand-writing the merged file.** It will drift from the standalone files the first time anything is edited. Merge from the same fragments.
- **Dropping the example to save room.** In an exam graded against model answers, a missing example loses its own mark. Shorten the example; never remove it.
- **Letting the recap lose the exam flags.** Confirmed-question markers and exam traps are exactly what a last-pass reader is scanning for — they should be *more* prominent here, not less.
- **Cutting content when the student says a topic is "too much".** They are almost always describing a *reading-order* problem, not a length problem. Rank it into tiers before you delete a single line, and check whether the complaint is really "which of this do I need for one question?"
- **Quoting a compression ratio for a merged recap-plus-answer-layer file.** It is bigger than its source by design, and saying otherwise destroys the student's trust in every other number you report.
