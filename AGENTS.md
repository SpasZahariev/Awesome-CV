# AGENTS.md

LaTeX project — personal CV / résumé / cover letters on the [Awesome-CV](https://github.com/posquit0/Awesome-CV) template. Owner: Spas Zahariev.

**Full guide:** see [`CLAUDE.md`](./CLAUDE.md). Human overview: [`README.md`](./README.md). Cover-letter recipe: [`.claude/skills/new-cover-letter/SKILL.md`](./.claude/skills/new-cover-letter/SKILL.md).

## Critical facts

- Compile with **xelatex**, not pdflatex (custom fonts).
- `awesome-cv.cls` lives at repo **root**. Files in subdirs (e.g. `cover-letters/`) must put it on `TEXINPUTS`.
- Cover letters + their PDFs live in `cover-letters/`. Real résumé content is modular in `examples/resume/*.tex` — mine it for letters.

## Compile a cover letter

```bash
cd cover-letters
TEXINPUTS=..:: xelatex -interaction=nonstopmode <name>-cover-letter.tex
rm -f <name>-cover-letter.aux <name>-cover-letter.log <name>-cover-letter.out
```

## Compile the résumé

```bash
xelatex -interaction=nonstopmode examples/resume.tex
```

## Rules

- ASCII only in `.tex` bodies; escape `& % #` as `\& \% \#`.
- Naming: `<company>-cover-letter.{tex,pdf}`, lowercase, in `cover-letters/`.
- Commit both `.tex` and built `.pdf`.
- Copy the contact block (`\name`, `\email`, ...) verbatim from an existing letter.
