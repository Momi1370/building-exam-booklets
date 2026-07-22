# Booklet Format & Build Mechanics

Reference for `building-exam-booklets`. The visual spec, the python-docx engine, survival tricks, and the verification gate.

## Visual format (the "DS4B" style the student passed with)

- **Body:** Times New Roman, 10pt. Plain full sentences, **one idea per line**. No wall-of-bullets.
- **Lecture banner** (one per module): a filled full-width table cell, ~22pt bold white text on a coloured fill. `b.lecture("LECTURE 1 · Introduction to BPM", BLUE)`.
- **Section header** `h2` / `h3`: 13.5pt bold, coloured — numbered `1.1`, `1.2` to mirror the lecture's own order.
- **Story/topic title** (optional, DS4B flavour): larger bold with an emoji.
- **Inline markers** parsed from text: `**bold**` anchors, `*italic*`, plus 🔑 key point, ⚠ trap, 🎯 flag, 🎓 professor's note.
- **Callouts:** a bordered table with a coloured left bar + heading. Types:
  - **🎓 PROFESSOR'S NOTE** (TEAL) — said only in the recording.
  - **🔑 KEY EXAM POINT** (GREEN), **⚠ EXAM TRAP** (RED), **✍ EXAM TIP** (AMBER), **🧠 MEMORY HOOK** (PURPLE, e.g. D-E-E-L).
- **🎯 Q&A FLAG** badge (magenta/purple) — placed at every concept the exam-info session pointed to.

### Palette (hex)
```
RED=C0392B  AMBER=E67E22  BLUE=2471A3  GREEN=1E8449
PURPLE=6C3483  GREY=566573  DARK=1B2631  TEAL=117A65  MAGENTA=8E44AD
```

## The answer-bank block (`examq`)

Each confirmed question / learning goal renders as:
```
Q3. [the question]                                    [🎯 flag tag]
✍ How to structure: <one line naming the parts the grader wants>
▸ <label> — <model-answer part, in course terms, with the example>
▸ <label> — <…>
⚠ Graders check: <exactly what loses marks if missing>
```
Signature: `examq(qnum, question, structure, parts=[(label,text),…], tag=None)`.

## The D-E-E-L answer skeleton (teach this in the booklet)
**D**efine (course definition) → **E**xplain (why/how it works) → **E**xample (the professor's case) → **L**ink (back to the case/course concept). Missing the second E is the top mark-loser.

## Self-contained python-docx engine

**Why self-contained:** `/tmp` gets wiped mid-session. Embed the engine in the build script (no `import engine`), and copy the finished `.docx` **and** the script to the session scratchpad after every build. Never rely on `/tmp` surviving.

```python
#!/usr/bin/env python3
# Self-contained booklet builder. No external engine import.
from docx import Document
from docx.shared import Pt, RGBColor, Inches
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.oxml.ns import qn
from docx.oxml import OxmlElement
import re

RED,AMBER,BLUE,GREEN="C0392B","E67E22","2471A3","1E8449"
PURPLE,GREY,DARK,TEAL,MAGENTA="6C3483","566573","1B2631","117A65","8E44AD"

def _shade(cell, hexcolor):
    sh = OxmlElement('w:shd'); sh.set(qn('w:val'),'clear'); sh.set(qn('w:fill'),hexcolor)
    cell._tc.get_or_add_tcPr().append(sh)

def _no_borders(tbl):
    t = tbl._tbl.tblPr; b = OxmlElement('w:tblBorders')
    for e in ('top','left','bottom','right','insideH','insideV'):
        el=OxmlElement(f'w:{e}'); el.set(qn('w:val'),'none'); b.append(el)
    t.append(b)

class Booklet:
    def __init__(self):
        self.d = Document()
        st = self.d.styles['Normal']; st.font.name='Times New Roman'; st.font.size=Pt(10)

    def _runs(self, para, text):
        # parse **bold** and *italic*
        for tok in re.split(r'(\*\*[^*]+\*\*|\*[^*]+\*)', text):
            if not tok: continue
            if tok.startswith('**') and tok.endswith('**'):
                r=para.add_run(tok[2:-2]); r.bold=True
            elif tok.startswith('*') and tok.endswith('*'):
                r=para.add_run(tok[1:-1]); r.italic=True
            else:
                para.add_run(tok)

    def lecture(self, text, color=BLUE):        # filled banner
        t=self.d.add_table(rows=1,cols=1); _no_borders(t); c=t.cell(0,0); _shade(c,color)
        p=c.paragraphs[0]; r=p.add_run(text); r.bold=True; r.font.size=Pt(22)
        r.font.color.rgb=RGBColor(0xFF,0xFF,0xFF); self.spacer()

    def h2(self, text, color=DARK):
        p=self.d.add_paragraph(); r=p.add_run(text); r.bold=True; r.font.size=Pt(13.5)
        r.font.color.rgb=RGBColor.from_string(color)

    def p(self, text):
        para=self.d.add_paragraph(); self._runs(para,text); return para

    def callout(self, heading, body, color=TEAL):
        t=self.d.add_table(rows=1,cols=1); cell=t.cell(0,0); _shade(cell,'F4F6F7')
        # coloured left bar
        tcPr=cell._tc.get_or_add_tcPr(); bd=OxmlElement('w:tcBorders')
        left=OxmlElement('w:left'); left.set(qn('w:val'),'single'); left.set(qn('w:sz'),'24')
        left.set(qn('w:color'),color); bd.append(left); tcPr.append(bd)
        hp=cell.paragraphs[0]; hr=hp.add_run(heading); hr.bold=True
        hr.font.color.rgb=RGBColor.from_string(color)
        self._runs(cell.add_paragraph(), body); self.spacer()

    def examq(self, qnum, question, structure, parts, tag=None):
        p=self.d.add_paragraph(); r=p.add_run(f"Q{qnum}. "); r.bold=True
        self._runs(p, question)
        if tag:
            tr=p.add_run(f"   {tag}"); tr.bold=True; tr.font.color.rgb=RGBColor.from_string(MAGENTA)
        s=self.d.add_paragraph(); sr=s.add_run("✍ How to structure: "); sr.bold=True
        self._runs(s, structure)
        for label,text in parts:
            pp=self.d.add_paragraph(); lr=pp.add_run(f"▸ {label} — "); lr.bold=True
            self._runs(pp, text)
        self.spacer()

    def image(self, path, width=5.5):
        try: self.d.add_picture(path, width=Inches(width))
        except Exception: self.p(f"[missing image: {path}]")

    def spacer(self): self.d.add_paragraph()
    def save(self, path): self.d.save(path)
```

## /tmp survival & image recovery

- After every build: `cp booklet.docx build_script.py <scratchpad>/`.
- If diagrams already live embedded in an existing `.docx` and the image folder was wiped, recover them:
  walk `Document(docx).inline_shapes` **in build order**, read each blob via
  `sh._inline.graphic.graphicData.pic.blipFill.blip.embed` → `part.related_parts[rId].blob`,
  and write it back under the filename your `b.image()` calls expect.

## Extract module text from an existing booklet
Banners live inside tables, not paragraphs. To pull a module's text between two banners, walk
`doc.element.body.iterchildren()`, compute full text for **both** `qn('w:p')` and `qn('w:tbl')`
blocks, and toggle capture on/off when a block's text matches a banner marker.

## Verification gate (run before saying "done")
```python
from docx import Document
d = Document(path); paras=[p.text for p in d.paragraphs]
txt="\n".join(paras)
assert "**" not in txt, "stray bold markers leaked"     # _runs failed somewhere
print("paras:", len([p for p in paras if p.strip()]),
      "| tables:", len(d.tables),
      "| images:", len(d.inline_shapes),
      "| stray '**':", txt.count("**"),
      "| examq blocks:", txt.count("✍ How to structure"))
# also eyeball: every lecture banner present, every 🎯 flag present,
# every image has explanatory prose near it, section order mirrors the lectures.
```
Confirm all of: **0 stray `**`**, every diagram present *and explained*, every banner + 🎯 flag present, section numbering mirrors the lecture order. Only then report done, with the counts.
