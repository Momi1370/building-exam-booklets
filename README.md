# building-exam-booklets

Two [Claude Code](https://claude.com/claude-code) **skills** that turn a university course's own materials into exam-ready study assets for **closed-book, open-question exams graded against the professor's model answers**:

1. **`building-exam-booklets`** — turns slide decks, lecture notes, transcripts, and study guidelines into a single colour-coded, exam-ready **Word booklet** (`.docx`) you read instead of the slides.
2. **`building-exam-reference-html`** — turns a topic of that (already-built, possibly hand-edited) booklet into a standalone, interactive **HTML study page** — clickable worked examples, a theme toggle, a purpose index — for the final review pass before the exam.

Use them together: build the booklet first, study from it (editing it yourself in Word as you go), then use the HTML skill to turn whichever topics you want a browsable last-mile review page for.

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
- Standard page shape: numbered nav chips, a purpose index, a consistent colour-coded callout taxonomy, clickable `<details>` blocks for every worked example, light/dark theme toggle.
- Runs a mandatory end-of-topic audit — checks heading numbering is sequential and unbroken, and diffs the source's section list against the HTML — since an ordinary edit can silently orphan a section under the wrong heading.

**Use:** once a topic exists in your booklet, say *"turn Topic 3 into an HTML reference page"*, or invoke `/building-exam-reference-html` directly.

## Install

You need [Claude Code](https://claude.com/claude-code) — this is instructions *for Claude*, not a standalone app.

```bash
git clone https://github.com/Momi1370/building-exam-booklets.git
cp -R building-exam-booklets/building-exam-booklets ~/.claude/skills/
cp -R building-exam-booklets/building-exam-reference-html ~/.claude/skills/
```

Then start (or restart) Claude Code — it auto-discovers any folder in `~/.claude/skills/`.

> On a shared team repo instead? Copy both skill folders to `.claude/skills/` inside that repo and everyone who clones it gets both skills.

## Requirements

- **Claude Code** (CLI, desktop, or IDE extension).
- **Python** with `python-docx`, for building the booklet and for reading it back via the mirror: `pip install python-docx`. Reading/using either skill's instructions doesn't need it; generating or re-reading the `.docx` does.

## What's inside

| File | Purpose |
|---|---|
| `building-exam-booklets/SKILL.md` | Booklet workflow, grading rules, and the Phase 6 handoff/audit discipline. |
| `building-exam-booklets/booklet-format.md` | The visual format spec, the runnable `python-docx` engine, and the verification checklist. |
| `building-exam-reference-html/SKILL.md` | HTML reference-page workflow: the section-by-section approval loop, procedural-vs-theoretical example style, page shape, and the end-of-topic audit. |

## License

MIT — use it, fork it, adapt it for your own courses.
