---
name: exam-prep-intake
description: Use at the START of any exam-prep work, before building or teaching anything, to scope the job in one round of questions and route to the right skill. Triggers include "help me study for this exam", "build study materials for this course", "I have an exam on X", "where do I start with this course folder", or any request that could plausibly be answered by building-exam-booklets, building-exam-reference-html, building-exam-recap-html, building-exam-answer-layer, or teaching-exam-sections.
---

# Exam Prep Intake

## Overview

The entry point for the `building-exam-*` family. It builds nothing. It spends **one round of questions** finding out what the student actually needs, then hands off to whichever skill fits.

It exists because the expensive failures in this family are not bad writing, they are **building the wrong artifact**. A full reference page for a student who only wanted a recap, an answer layer shaped like the wrong professor's marking scheme, forty pages of tool instructions for an exam written on paper. Every one of those costs hours and is invisible until the student says "that is not what I meant."

## Core principle

**Detect what you can, ask only what you cannot, and never ask more than four questions.**

Anything discoverable by reading the folder is not a question. File formats, topic names, which lectures exist, whether there is a transcript, how many practice sessions there are: read them. Confirm what you found in one line and move on.

What you genuinely cannot detect: what the student wants *made*, how much time is left, what the exam is like, and how their mind works. Those are the questions.

## Workflow

### 1. Read the folder before asking anything

List the course directory. Identify, without asking:

- The topic or lecture structure, and how many there are
- Which source types exist per topic: decks, lecture-notes PDFs, transcripts, practicals, study guidelines, past exam questions
- Whether any study assets already exist from earlier sessions (booklets, HTML pages, question banks)
- Whether a professor is named anywhere, and whether **different topics have different professors**

Then state what you found in about three lines. This is not a report, it is a receipt: it proves you looked, and it lets the student correct a wrong reading before it costs anything.

### 2. Ask one round, at most four questions

Use a single multiple-choice round. These four earn their place; drop any whose answer you already have.

**Q1 — What should I build?** The routing question, and the most valuable of the four.
- A **Word booklet** you read instead of the slides → `building-exam-booklets`
- A **full HTML page** to learn from, section by section → `building-exam-reference-html`
- A **recap page** to re-read fast, with a compact answer above every question → `building-exam-recap-html` **merged with** `building-exam-answer-layer`
- **Nothing. Teach me** → `teaching-exam-sections`

Offer the merged recap-plus-answer-layer as **one option, not two**. Students who want a recap almost always also want the compact answers, and maintaining two files per topic is what makes them distrust both.

**Q2 — Tell me about the exam.** Open-ended, and worth more than any other single answer.
Ask for: date, length, closed or open book, written by hand or typed, roughly how many questions, whether it is open questions, multiple choice, True/False, or a mix, and **anything they remember from a previous sitting**. A resit student's memory of the real paper outranks every study guide.

**Q3 — How long should an answer be?** Short, long, or both.
"Both" means the two-speed page: a compact writable answer on top, the full one collapsed underneath. It is the right default for a written exam and should be labelled as recommended.

**Q4 — Do you want the topics connected?** Whether to build cross-topic links.
Worth asking because it is real work and not always wanted. If yes, it produces two things: a per-section "related in other topics" strip, and one shared table of **terms that mean different things in different topics**. If the student is sitting two courses close together, ask whether the *other* course should be compared too. Overlapping vocabulary between two courses taken in the same month is a genuine source of lost marks.

### 3. Ask the scope questions the folder raised

Not part of the fixed four. Ask only when the folder actually poses the question:

- **Practicals and tools.** If the practice sessions teach specific software, ask whether the tools are examinable. Usually they are not and the exam is on paper, in which case **keep the technique and drop the tool**: the SQL, the alignment table, the hand-drawn diagram stay; the click-paths and node names go.
- **Several professors.** If different topics have different lecturers, say so and treat their answer shapes separately (step 5).
- **A pre-existing artifact.** If a booklet or page already exists, confirm whether it is the source of truth or something to be replaced. If the student has hand-edited it, it is **theirs**: read it through a plain-text mirror and never write back to it.

### 4. Read everything, then propose the priority order

Now read the sources properly. Then, before building, give the student a **ranked plan**, not a flat list. Rank by:

1. **Confirmed past questions** first. What actually appeared outranks everything.
2. Then everything in the lectures.
3. Then the study guide's emphasis. A study guide tells you where the weight is, **not what is excluded**.

If the exam is close, say plainly what you would cut and why. Scaling the work down is the student's call, but the recommendation is yours to make.

### 5. Derive the answer shape from the professor, do not import one

Before writing a single answer, work out what **this** professor rewards, from their own materials:

- Their **question verbs**, collected from review slides, sample questions and past papers. "In your own words explain", "how is it constructed", "why is it important", "suppose", "give a concrete example", "what are the risks" describe a very specific answer order, and it is not the same order another lecturer wants.
- Any **officially named question styles**. Some courses publish them, for example *reproduce / relate / translate to an example / apply the technique*. If they exist, tag every answer with which style it is.
- Any **published model answer**, because its layout is the marking structure. If the official solution is laid out in three numbered steps, three numbered steps is the format.

Never carry an answer shape over from a different course or a different lecturer. Two professors on the same paper need two shapes.

### 6. Build one section, stop, and wait

Build **one** section, or one question, complete and in its final form. Show it. Wait for explicit approval.

This is the rule that already governs `building-exam-reference-html` and `building-exam-answer-layer`, and it belongs to the whole family: a topic can hold forty sections, and rebuilding all of them because the shape was wrong is the most expensive mistake available. Settle the shape on one.

Once approved, build the rest without stopping at every section.

## Handing off

Say which skill you are handing to and why, in one line. Then invoke it. Carry forward, so the next skill does not re-ask:

- the artifact chosen, and the format
- the exam's logistics and any confirmed past questions
- the professor's answer shape, per professor
- the scope rulings, especially what is out
- the answer length, and whether cross-topic links are wanted

## Two things to carry into every build

**Triage beats deletion.** When a topic turns out longer than its exam weight, do not cut the content, **rank** it: a tier the student must write cold, a tier to recognise, and a tier to read once and skip on the last pass, each with a minute budget. Content the sources support should stay on the page; what the student needs is a reading order, not a smaller file. A topic worth one exam question can still deserve eight sections, as long as the page says which three matter.

**A merged recap-plus-answer-layer file is larger than the reference page it came from, by design.** It carries a compact answer, the full answer, and the drills. Reporting a "compression ratio" for it is misleading. Report band count, word count, and audit results instead.

## Common mistakes

- **Asking what the folder already answers.** "What documents do you have" is a bad question when you can list the directory. It reads as not having looked.
- **Interrogating before delivering anything.** More than four questions up front is its own failure. Ask once, then produce something.
- **Skipping the intake because the request sounds obvious.** "Make me a study page" hides at least three decisions: which format, which depth, and which professor's answer shape.
- **Building the artifact you find most interesting.** The routing question exists because a full reference page is more satisfying to build and often not what was asked for.
- **Treating the study guide as a fence.** It marks emphasis, not boundaries. Confirmed past questions routinely land on material no learning goal mentions.
- **Carrying one professor's answer structure into another's topic.** Derive it every time, from that lecturer's own question wording.
- **Deleting content when a topic feels too long.** Rank it instead.
