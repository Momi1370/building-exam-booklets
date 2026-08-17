---
name: building-exam-reference-html
description: Use when a student wants a booklet topic turned into a browsable HTML study page, or wants to review/verify/expand an existing topic HTML reference file section by section against its authoritative booklet — for both procedural (SQL, calculations) and purely theoretical (frameworks, definitions, theory comparisons) course topics.
---

# Building Exam Reference HTML

> **Start with `exam-prep-intake`** if the scope is not already settled. It asks one round of questions (what to build, what the exam is like, answer length, cross-topic links), derives the professor's answer shape, and hands over. Skip it only when those answers are already in hand.

## Overview

Turn one topic of an already-approved exam booklet into a standalone, interactive HTML page the student reads instead of the booklet or slides before a closed-book exam. Complements `building-exam-booklets` (which builds the `.docx`) — this is the downstream, browsable layer.

## Core principle

**Build it incrementally, section by section, with the student — never dump a finished page in one autonomous shot.** For each numbered subsection: teach or clarify it, offer a clean short version, wait for explicit approval, then write only that into the HTML. Don't write ahead of what's been approved, even if you could produce a good page unprompted.

## Workflow

1. **Read only, never edit the source.** If the booklet is a `.docx`, read it through a read-only plain-text mirror (extract once with a script, regenerate whenever the student edits the source). Never write to the `.docx` itself.
2. **Cross-verify against the real original materials** whenever they exist — slide decks, lecture notes, transcripts. Don't trust the booklet text as ground truth; it can itself have gaps (merged headings, content that was assigned but never actually written in). Image-heavy slides need rendering (e.g. `pdftoppm`), not just `pdftotext` — diagrams carry real content that text extraction misses.
3. **Number sections exactly like the source** (e.g. "(3.6)") so the student can cross-reference. A wrong or dropped number is the most common self-inflicted bug — verified at the end (step 6), not assumed.
4. **Match depth and example style to what the section needs:**
   - *Procedural/technical* (SQL, formulas, calculations): one full worked example **per variant**, each in a clickable block, following the exact real-world "formula" the grader expects, same structure every time — this kind of content lives or dies on syntax fidelity for a handwritten exam.
   - *Theoretical* (frameworks, definitions, theory comparisons): one applied/classification example per concept the student could confuse with another, plus a compare/contrast table for anything easy to conflate (two theories, two definitions). A short self-test ("classify this new example") is the theory-equivalent of a worked example — often teaches more than restating the definition again.
   - *Easy/background* sections: 2-4 sentences, don't over-build.
5. **Standard page shape:** numbered nav chips; a "Purpose index" section listing every subsection as a one-line "Purpose: ..." (matches how exam prompts are phrased); a consistent callout taxonomy — Definition / Key exam point / Exam trap / Exam tip / Memory hook / Professor's note, each its own color; `<details class="q">` for every worked example or practice question so the page stays scannable; light/dark theme toggle.
   - **Size the reading column at `max-width: ~1240px`, not the ~800px a default shell gives you.** `max-width` is a ceiling, not a fixed width, so widening it cannot break the phone layout: a narrow screen still gets the full viewport exactly as before. At 820px the text sits in a strip about 13cm wide on a laptop and the student ends up zooming on every pass. Set it at build time, because retrofitting it later means re-checking every fixed-width block (tables, `<pre>`) whose line lengths were tuned to the old column.
6. **End-of-topic audit — mandatory, not optional.** Grep every `<h2>/<h3>` and confirm the numbering is sequential and unbroken (an earlier edit can silently orphan a section's content under the wrong heading). Then diff the source's full section list against the HTML to catch anything dropped, never resolved from an earlier offer, or left as a stray unlabeled block. Report findings — don't assume it's fine because it was built carefully.

## Common mistakes

- **Dumping the whole page in one shot.** Skips the approve-per-section loop the student actually wants.
- **Reusing the procedural "one example per variant" pattern verbatim for theory topics.** Theory needs classification/compare-contrast, not a syntax drill dressed up differently.
- **Trusting the booklet text over the real slides when both exist.** The booklet is a compiled artifact, not the primary source — treat mismatches as bugs to report, not the slides as wrong.
- **Leaving the page at a default narrow column.** An 800px-ish `max-width` looks fine in a preview and reads as a thin strip on a real laptop, so the student zooms on every pass. Widening it is safe for phones (see the page-shape rule) and costs nothing, so do it in the first build.
- **Skipping the end-of-topic audit** because the page "was built carefully." Structural bugs (a section silently orphaned under the wrong heading) happen from ordinary editing and are invisible unless specifically checked.
