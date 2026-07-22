# building-exam-booklets

A [Claude Code](https://claude.com/claude-code) **skill** that turns a university course's own materials — slide decks, lecture notes, study guidelines, Q&A / voice transcripts, image-heavy slides — into a single colour-coded, **exam-ready study booklet** (a Word `.docx`) that you read instead of the slides and can compare line-by-line against your own lecture notes.

It's built for **closed-book, open-question exams that are graded against the professor's model answers**, so every explanation is written in course terminology, always followed by an example, with the confirmed exam questions answered inline.

## What it does

- Maps the course folder (slides, lecture notes, `Voice.rtf` recordings, handbook chapters, practicals, study guidelines, past Q&A).
- Reads the **study guidelines** (learning goals → exam questions) and the **Q&A / exam-info session** (grading rules + confirmed questions).
- **Learns image-heavy slides** (frameworks, diagrams, canvases) and explains them in prose instead of skipping them.
- Diffs slides vs lecture **notes** vs the **voice recording** so nothing examinable is missed.
- Writes it lecture-by-lecture in a colour-coded format (banners, section numbers mirroring the lecture, Define → Explain → Example, professor's-note and exam-flag callouts).
- Builds the `.docx` with a self-contained `python-docx` engine and verifies the output.

## Install

You need [Claude Code](https://claude.com/claude-code) — this is instructions *for Claude*, not a standalone app.

```bash
git clone https://github.com/Momi1370/building-exam-booklets.git
cp -R building-exam-booklets/building-exam-booklets ~/.claude/skills/
```

Then start (or restart) Claude Code — it auto-discovers any folder in `~/.claude/skills/`.

> On a shared team repo instead? Copy the `building-exam-booklets/` folder to `.claude/skills/` inside that repo and everyone who clones it gets the skill.

## Use

Open Claude Code in the folder that holds your course materials and say:

> build an exam booklet for this course

or invoke it directly with `/building-exam-booklets`.

## Requirements

- **Claude Code** (CLI, desktop, or IDE extension).
- **Python** with `python-docx` for the final build step only: `pip install python-docx`. (Reading/using the skill doesn't need it; generating the Word file does.)

## What's inside

| File | Purpose |
|---|---|
| `building-exam-booklets/SKILL.md` | The workflow + grading rules (what Claude follows). |
| `building-exam-booklets/booklet-format.md` | The visual format spec, the runnable `python-docx` engine, and the verification checklist. |

## License

MIT — use it, fork it, adapt it for your own courses.
