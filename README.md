<h1 align="center">Spas Zahariev — CV & Cover Letters</h1>

<p align="center">
  Personal résumé, CV, and cover letters built on the
  <a href="https://github.com/posquit0/Awesome-CV">Awesome-CV</a> LaTeX template.
</p>

---

## What's here

| Path | Purpose |
|------|---------|
| `awesome-cv.cls` | The Awesome-CV template class (root-level — every `.tex` depends on it). |
| `examples/resume.tex` | Main résumé. Composed from modular sections. |
| `examples/resume/*.tex` | Résumé content: `summary`, `experience`, `skills`, `education`, `certificates`, … Edit these. |
| `cover-letters/` | Cover letter sources (`.tex`) and built PDFs. |
| `Makefile` | Builds the `examples/` docs (uses `lualatex`). |
| `2021/` | Archived older CV PDF. |

## Requirements

A TeX distribution with **XeLaTeX** and the custom fonts (Roboto, Source Sans Pro, FontAwesome). On this machine (NixOS) `xelatex` is already on `PATH`; otherwise install `texlive-full` or use the [TeX Live Docker image](https://hub.docker.com/r/texlive/texlive).

## Building

### Résumé

```bash
xelatex -interaction=nonstopmode examples/resume.tex
# or, via Makefile (lualatex):
make resume.pdf
```

### A cover letter

Cover letters sit in `cover-letters/`, one level below the class file, so point `TEXINPUTS` at the root:

```bash
cd cover-letters
TEXINPUTS=..:: xelatex -interaction=nonstopmode sygnum-cover-letter.tex
```

This produces `sygnum-cover-letter.pdf` in the same folder. Clean up build artifacts (`*.aux *.log *.out`) afterward — they're gitignored.

## Creating a new cover letter

Copy an existing letter (e.g. `cover-letters/sygnum-cover-letter.tex`), swap the recipient and the three body sections, then compile as above. Agents can run the **`new-cover-letter`** skill for the full guided procedure — see `.claude/skills/new-cover-letter/SKILL.md`.

## For AI agents

Start with [`CLAUDE.md`](./CLAUDE.md) / [`AGENTS.md`](./AGENTS.md) — project layout, conventions, and the exact compile commands.

## Credit

Template: [Awesome-CV](https://github.com/posquit0/Awesome-CV) by [posquit0](https://github.com/posquit0), licensed CC BY-SA 4.0. See `LICENCE`.
