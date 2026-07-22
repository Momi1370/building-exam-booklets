---
name: building-exam-booklets
description: Use when the user wants an exam-ready study booklet built from a university course's own materials — slide decks, lecture notes, study guidelines, Q&A or voice transcripts, image-heavy slides — for a closed-book open-question exam graded against the professor's model answers. Triggers include "build an exam booklet", "summarize this course for my exam", "apply the MPP booklet format to <course>", "compare my notes to a booklet".
---

# Building Exam Booklets

## Overview

Turn a university course's raw materials into a single colour-coded, exam-ready `.docx` booklet the student reads instead of the slides — and can diff line-by-line against their own lecture notes.

**Core principle — two non-negotiables:**
1. **Grounded in THIS course's own materials.** Every concept, example, and diagram comes from the course's slides / lecture notes / voice recordings / handbook — never generic web knowledge or a different framework. The student compares the booklet against their notes; anything not traceable to the course is worse than useless.
2. **Written the way the professor grades.** Explanations are in the student's own words but strictly in **course terminology**, and every concept is followed by an **example**. Professors mark rigidly against their own model answer (see Grading Rules below).

This is the "MPP booklet" format (course 5067). It generalises to any lecture-based course.

## The Workflow (do the phases in order)

### Phase 0 — Map the materials
List the course folder. UHasselt courses follow a consistent layout; expect per lecture:

| File | What it is | Weight |
|---|---|---|
| `Slide Deck …pdf` / `Module N … Slides.pdf` | Lecture slides | Primary |
| `Lecture Notes …pdf` | Prose notes | **Often richer than slides — exam material** |
| `Voice.rtf` / `voice.rtf` / `.mov` | Recording transcript | Professor asides, examples, "this is on the exam" |
| Handbook chapter / article `.pdf` | Named in the study guide | Exam material where indicated |
| Practical session assignments (+ *with solutions*) | Exercises | Exam exercises mimic these |
| `Study guidelines … .docx` | **Content & Learning goals per module** | **Defines what is examinable** |
| Q&A / exam-info session deck + `Q&A.rtf` | Exam-info session | **Defines the grading rules & confirmed questions** |
| `Sample exam questions … .docx` | Past questions | Highest-value |

Read the **study guidelines** first: the professor turns each "Content and Learning goal" into an exam question (sometimes combining two). Read the **Q&A/exam-info session** second: it gives the exam format, how questions are built, confirmed questions, and the grading rubric.

### Phase 1 — Learn the content, especially image-heavy slides
Extract text with `pdftotext`, but **text extraction misses diagrams**. When a slide is mostly a picture/diagram with little text (value chains, frameworks, canvases, network diagrams), **open and read the rendered image**, understand the framework it teaches, then **explain it in prose**. Never paste "[image]" or skip a diagram — learn it, then teach it. **Diff the slides against the lecture NOTES and the voice transcript**; notes usually contain examinable detail absent from slides, and the recording contains professor examples/asides found nowhere else.

### Phase 2 — Lock in the grading rules
From the Q&A/exam-info materials, capture the exact rubric and the confirmed/flagged questions. These govern how *every* answer paragraph in the booklet is written. Store them as a memory (project type) so they survive across sessions.

### Phase 3 — Write it, lecture by lecture, in the format
For each lecture/module produce, in order:
- a **coloured lecture banner** (one per module),
- small **section headers** (`1.1`, `1.2`, …) mirroring the lecture's own order so it diffs against the student's notes,
- **plain readable prose, one idea per line** — focus on the *most important (examinable)* points, don't transcribe everything,
- each concept as **Define → Explain → Example**, with the **example inline directly under the concept** (use the professor's own example when the lecture gives one; a real-life one only when it doesn't),
- **source tags woven into the prose** ("from the slides", "the professor noted in class", "exam material = notes + slides + <article>"),
- a **🎓 PROFESSOR'S NOTE** callout for anything said only in the recording,
- a **🎯 Q&A FLAG** badge at every spot the exam-info session pointed to.

### Phase 4 — Answer the confirmed questions and learning goals
Answer every confirmed exam question **inline at its concept** (🎯 marker), and maintain a separate structured **answer-bank** file: each entry = *Question → ✍ how to structure → labelled model-answer parts → ⚠ what graders penalise*. Turn **every** study-guide learning goal into one such Q+answer.

### Phase 5 — Build and verify
Build with a **self-contained** python-docx script (see `booklet-format.md`) and verify before claiming done.

## Grading Rules (drive every answer)

1. **Own words, but course terminology only.** A "generally correct" answer that uses a different framework loses marks.
2. **Always give the example.** If a question asks for one and you omit it, you lose that part's marks — no exceptions.
3. **Answer every part / component.** Explanation *and* example, and each sub-item named.
4. **Concise ≠ superficial.** Master's level: say what actually happens, not five words.
5. **Exercises: logic and sequence earn the marks.** A slightly-off final number still scores if the method is right; a wildly wrong one scores 0. Show every step.

Memory hook to teach in the booklet: **D-E-E-L** — Define → Explain → Example → Link (to the case/course).

## Format & build mechanics

The full DS4B format spec (palette, banner/callout/flag styles, the `examq` answer-bank block, the D-E-E-L guide) **and** the python-docx engine recipe, /tmp-cleanup survival, image recovery, and the verification checklist live in **`booklet-format.md`** — read it before building.

## Common Mistakes

- **Skipping or "[image]"-ing a diagram-heavy slide.** Learn the diagram, then explain it. This is where the most exam value hides.
- **Generic/web answers.** Traceable-to-course-or-cut. If it's not in the slides/notes/handbook, don't put it in.
- **Dropping the example** to save space. That's the single most common way to lose marks.
- **Reordering away from the lecture.** Mirror the lecture's own section order so the student can diff against their notes.
- **A non-self-contained build script.** `/tmp` gets wiped mid-session; embed the styling engine and back up to the scratchpad (see `booklet-format.md`).
- **Claiming done without verifying** 0 stray asterisks / all images present & explained / all banners & flags present.
