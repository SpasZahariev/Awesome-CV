# CLAUDE.md — Agent Guide

LaTeX project. Personal CV, résumé, and cover letters built on the [Awesome-CV](https://github.com/posquit0/Awesome-CV) template. Owner: **Spas Zahariev** (Zurich, Switzerland).

> Also read `AGENTS.md` (same critical facts, short) and `README.md` (human-facing overview).

## Layout

```
awesome-cv.cls              # The template class. Root-level. Every .tex needs it on TEXINPUTS.
Makefile                    # Builds examples/ only, with lualatex (upstream default).
cover-letters/              # <-- Cover letter .tex + built .pdf live here. Main working dir.
  sygnum-cover-letter.tex   # Reference letter — copy its structure for new ones.
  *-cover-letter.pdf        # Built output. Keep committed.
examples/
  resume.tex                # Main résumé. Pulls modular content via \input.
  resume/*.tex              # summary, experience, skills, education, certificates, ... (edit these)
  cv.tex, coverletter.tex   # Upstream template samples.
2021/                       # Old exported CV pdf. Archive.
```

Résumé content is **modular**: edit `examples/resume/experience.tex`, `skills.tex`, `summary.tex`, etc. — not `resume.tex` itself (that only `\input`s them). This is the source of truth for Spas's real experience; mine it when writing cover letters.

## Compiling — use xelatex

Template needs **xelatex** (custom fonts: Roboto, Source Sans Pro, FontAwesome). Not pdflatex.

**Cover letter** (in a subdir, so class file is one level up — set `TEXINPUTS`):
```bash
cd cover-letters
TEXINPUTS=..:: xelatex -interaction=nonstopmode <name>-cover-letter.tex
```
The trailing `::` keeps the default search path; `..` adds the root so `awesome-cv.cls` resolves. Output: `<name>-cover-letter.pdf` in the same dir.

**Résumé / root-level docs** (class file already alongside):
```bash
xelatex -interaction=nonstopmode examples/resume.tex   # or: make resume.pdf (uses lualatex)
```

`-interaction=nonstopmode` stops LaTeX from hanging on a prompt when `.cls` is missing — errors print and it exits.

### After compiling
Delete build junk (already gitignored, but keep the dir clean):
```bash
rm -f <name>.aux <name>.log <name>.out
```
Commit the `.tex` **and** the `.pdf`.

## Conventions

- **Naming:** `<company>-cover-letter.tex` / `.pdf`, all lowercase, in `cover-letters/`.
- **Color:** `\colorlet{awesome}{awesome-lavender}` — keep consistent across docs.
- **ASCII only** in `.tex` bodies. No stray Unicode/CJK — it breaks the build or renders as tofu. Escape `&` → `\&`, `%` → `\%`, `#` → `\#`.
- **Contact block** (`\name`, `\mobile`, `\email`, `\homepage`, `\github`, `\linkedin`): copy verbatim from an existing letter. Don't invent values.

## Making a new cover letter

Use the **`new-cover-letter` skill** (`.claude/skills/new-cover-letter/SKILL.md`) — it's the canonical procedure. In short: fetch the job post → copy `sygnum-cover-letter.tex` → rewrite recipient + 3 sections from résumé facts → compile with the xelatex command above → clean aux files.
