# building-exam-booklets

Four [Claude Code](https://claude.com/claude-code) **skills** that turn a university course's own materials into exam-ready study assets for **closed-book, open-question exams graded against the professor's model answers**:

1. **`building-exam-booklets`** — turns slide decks, lecture notes, transcripts, and study guidelines into a single colour-coded, exam-ready **Word booklet** (`.docx`) you read instead of the slides.
2. **`building-exam-reference-html`** — turns a topic of that (already-built, possibly hand-edited) booklet into a standalone, interactive **HTML study page** — clickable worked examples, a theme toggle, a purpose index — for the final review pass before the exam.
3. **`building-exam-recap-html`** — compresses that page into a **fast-recap layer**: one short page per module plus a merged all-modules page, for the fifth pass and the morning of the exam.
4. **`building-exam-answer-layer`** — turns that recap into **writing practice**: a compact, writable exam answer above every question with the full one collapsed beneath, plus a trigger sheet mapping question phrasing to the framework it wants.

Use them in order: build the booklet first, study from it (editing it yourself in Word as you go), then turn whichever topics you want into a browsable HTML page, compress that into a recap you can re-read in minutes, and finally add the answer layer once the problem stops being *knowing* the material and becomes *writing it fast enough*.

**Learn → browse → re-read → rehearse.** Each skill assumes the one before it is done.

**Two HTML versions, and you pick per topic:**

| | `building-exam-reference-html` | `building-exam-recap-html` | `building-exam-answer-layer` |
|---|---|---|---|
| **For** | Learning a topic properly | Re-reading a topic you already know | Writing it fast enough on the day |
| **Reading pass** | 1st–3rd | 4th and later, exam morning | Last week, once the content is solid |
| **Solves** | "I don't understand this yet" | "Re-reading takes too long" | "I know it, I just can't write it in six minutes" |
| **Depth** | Full explanation, worked examples, self-tests | One line per section, then the details you actually forgot | Both: a compact writable answer on top, the full one collapsed underneath |
| **Built** | Section by section, with your approval each time | Compressed from the finished full page | Derived question by question from the answers already there |

You do not have to choose once and for all. Build the full page for every topic, then add the recap layer only for the topics you keep re-reading, and the answer layer only if the exam's clock turns out to be the real constraint.

## 1. `building-exam-booklets`

Every explanation is written in course terminology, always followed by an example, with confirmed exam questions answered inline.

- Maps the course folder (slides, lecture notes, `Voice.rtf` recordings, handbook chapters, practicals, study guidelines, past Q&A).
- Reads the **study guidelines** (learning goals → exam questions) and the **Q&A / exam-info session** (grading rules + confirmed questions).
- **Learns image-heavy slides** (frameworks, diagrams, canvases) and explains them in prose instead of skipping them.
- Diffs slides vs lecture **notes** vs the **voice recording** so nothing examinable is missed.
- Writes it lecture-by-lecture in a colour-coded format (banners, section numbers mirroring the lecture, Define → Explain → Example, professor's-note and exam-flag callouts).
- Builds the `.docx` with a self-contained `python-docx` engine and verifies the output.
- **After handoff, the booklet becomes your own document.** Once you start hand-editing it in Word across study sessions, Claude switches to read-only: it builds a plain-text mirror to re-read what you actually have, and never writes to the `.docx` again. Later sessions become recurring audit passes — re-teaching a topic against the real slides, adding a full step-by-step **DEPTH** block under any section that turned out too compact to actually learn from, and flagging real gaps.

**Use:** open Claude Code in the folder with your course materials and say *"build an exam booklet for this course"*, or invoke `/building-exam-booklets` directly.

## 2. `building-exam-reference-html`

Once a booklet topic is solid, turn it into a page you actually read on your laptop the night before the exam.

- Works section by section **with you** — teaches or clarifies a subsection, proposes a short version, waits for your approval, only then writes it. Never dumps a finished page unprompted.
- Reads the booklet read-only (same mirror discipline as above) and cross-checks against the real slides/notes whenever they're available — the booklet is a compiled artifact, not automatically ground truth.
- Adapts example style to the content: **procedural** topics (SQL, formulas, calculations) get one full worked example per variant, in the exact real-world "formula" the grader expects; **theoretical** topics (frameworks, definitions, theory comparisons) get one applied/classification example per concept that's easy to confuse with another, plus compare/contrast tables and short self-tests.
- Standard page shape: numbered nav chips, a purpose index, a consistent colour-coded callout taxonomy, clickable `<details>` blocks for every worked example, light/dark theme toggle, and a wide reading column (`max-width: ~1240px`) so the text isn't a thin strip you have to zoom into on a laptop. Because `max-width` is a ceiling rather than a fixed width, the phone layout is unchanged.
- Runs a mandatory end-of-topic audit — checks heading numbering is sequential and unbroken, and diffs the source's section list against the HTML — since an ordinary edit can silently orphan a section under the wrong heading.

**Use:** once a topic exists in your booklet, say *"turn Topic 3 into an HTML reference page"*, or invoke `/building-exam-reference-html` directly.

> Once that page is solid, skill 3 compresses it into a re-read layer — see below.

## 3. `building-exam-recap-html`

The full page is where you *learn* a topic. By the fifth pass you don't need the explanation any more — you need the eight lines that fire the whole module back into your head. That's this skill.

It produces one condensed page per module plus a merged all-modules page, and its governing rule is that **compaction is subtraction of prose, never of gradable content**. What gets cut is connective tissue — build-up sentences, an idea phrased twice, the paragraph wrapped around an anecdote. What survives untouched is anything a grader could ask for.

How it compresses:

- **A "spine" opens every module** — one line per numbered subsection, stating that section's single load-bearing claim. Read the spine; drop into a section only when a line doesn't fire.
- **Prose becomes term → gloss rows** — bold term, one-line gloss. Characteristics, constraints, criteria, phases, framework components. The biggest space win, and it reads faster than the prose did.
- **Anecdotes shrink to their trigger phrase.** The professor's stories are memory anchors, so they stay — as a clause, not a paragraph.
- **Practice questions collapse to one-line answer skeletons** — the moves, arrow-separated, structural verbs bolded.
- **Tables stay at full size.** They're already the fastest thing on the page, and in this kind of exam each row is usually its own gradable point. Cutting rows buys no time and costs marks.
- **Denser typography than the full page**, so you can feel which pass you're on — but the same colour-coded flags, so confirmed-question markers and exam traps stay recognisable across both versions.

It's built as **content fragments plus a small assembler** holding the shared CSS and the merge, so the per-module files and the merged file can't drift apart. The end-of-topic audit diffs the recap's section list against the full page's, checks tags and links in every file including the merge, and then reports the compression ratio per module.

**That ratio is information, not decoration.** From a real 5-module project-management topic:

| File | Sections | vs full page |
|---|---|---|
| `Module1_Recap.html` | 1.1–1.8 | 56% |
| `Module2_Recap.html` | 2.1–2.5 | 65% |
| `Module3_Recap.html` | 3.1–3.5 | 55% |
| `Module4_Recap.html` | 4.1–4.4 | **71%** |
| `Module5_Recap.html` | 5.1–5.6 | 64% |
| **`ALL_Recap.html`** | **1.1–5.6** | **62% — 38% shorter overall** |

Module 4 barely compressed, and that's the point: it was earned-value calculations, a solved worked example and fixed step-lists — content that was already at minimum size. A module that refuses to shrink is telling you it was dense to begin with. Forcing every module to the same ratio would mean over-cutting that one.

**Use:** once a topic's full HTML page is finished, say *"make a shorter recap version of this"* or *"merge the modules into one recap page"*, or invoke `/building-exam-recap-html` directly.

## 4. `building-exam-answer-layer`

The recap tells you what is true. It still does not tell you what to **write** when there are 28 questions and 180 minutes.

This skill adds two things to a finished page. Every question and every worked exercise gains a compact **`⚡ Exam answer`** band at the top: telegraphic, aligned columns, keyword-dense, the example kept, stamped with a realistic `~N min` and what is actually graded. The answer that was already there is not deleted, it moves into a collapsed **`▸ the long version, for learning`** underneath. The page becomes two-speed: learn from the long version once, then only ever re-read the compact one.

The file also gains a collapsed **`⚡ Trigger sheet`** at the top, mapping *how a question is phrased* to *which framework to reach for*, with a link that opens the full answer.

What makes it work:

- **It starts from the exam's real logistics.** Question count, duration, marks per question, pages. The minutes-per-question figure that falls out is the specification for how long every band may be. Without it, "compact" is just another opinion about length.
- **Compact answers are derived, never rewritten.** A separately authored short answer drifts from the long one and the student stops trusting both.
- **Bands are deliberately over-provisioned, ordered so the cut comes from the bottom.** The framework's own words go at the top and the polish at the end, so stopping two thirds of the way down still leaves a scoring answer. Give the student something to cut rather than something to run out of.
- **Time estimates are per question, from counting graded elements.** A definition is 3 minutes; a draw-plus-apply is 10. A flat number makes every band the wrong length.
- **The example always survives.** In an exam graded against model answers it carries its own mark. Shorten it, never drop it.
- **The trigger sheet's left column is phrasings, not concept names.** *"Why does this keep going wrong"*, not *"root-cause analysis"*. A sheet keyed on concept names is a glossary, and the student did not need a glossary.

It also says the honest thing out loud: you rarely have to detect a framework from nothing, because most questions name the tool. That sentence removes more anxiety than the sheet itself does.

**Use:** once a topic's recap is solid, say *"I can't write these fast enough, make a compact exam-answer version"*, or invoke `/building-exam-answer-layer` directly.

## Install

You need [Claude Code](https://claude.com/claude-code) — this is instructions *for Claude*, not a standalone app.

```bash
git clone https://github.com/Momi1370/building-exam-booklets.git
cp -R building-exam-booklets/building-exam-booklets       ~/.claude/skills/
cp -R building-exam-booklets/building-exam-reference-html ~/.claude/skills/
cp -R building-exam-booklets/building-exam-recap-html     ~/.claude/skills/
cp -R building-exam-booklets/building-exam-answer-layer   ~/.claude/skills/
```

Then start (or restart) Claude Code — it auto-discovers any folder in `~/.claude/skills/`.

Install only what you need — the four are independent folders. The booklet skill stands alone; `building-exam-recap-html` expects a page built by `building-exam-reference-html` to compress; `building-exam-answer-layer` edits whichever HTML page you already have.

> On a shared team repo instead? Copy the skill folders to `.claude/skills/` inside that repo and everyone who clones it gets them.

## Requirements

- **Claude Code** (CLI, desktop, or IDE extension).
- **Python** with `python-docx`, for building the booklet and for reading it back via the mirror: `pip install python-docx`. Reading/using either skill's instructions doesn't need it; generating or re-reading the `.docx` does.

## What's inside

| File | Purpose |
|---|---|
| `building-exam-booklets/SKILL.md` | Booklet workflow, grading rules, and the Phase 6 handoff/audit discipline. |
| `building-exam-booklets/booklet-format.md` | The visual format spec, the runnable `python-docx` engine, and the verification checklist. |
| `building-exam-reference-html/SKILL.md` | HTML reference-page workflow: the section-by-section approval loop, procedural-vs-theoretical example style, page shape, and the end-of-topic audit. |
| `building-exam-recap-html/SKILL.md` | Recap-layer workflow: what compresses and what must not, the spine, the fragments-plus-assembler build, and the ratio audit. |
| `building-exam-answer-layer/SKILL.md` | Answer-layer workflow: the exam-logistics intake, how a compact answer is derived and stamped, the trigger sheet, and the depth-2 audit. |

## License

MIT — use it, fork it, adapt it for your own courses.
