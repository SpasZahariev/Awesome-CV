# Agent guide — Awesome-CV

This repository is the **Awesome CV** LaTeX class and example documents: résumé, CV, and cover letter. Work centers on `.tex` sources and `awesome-cv.cls`, not application code.

## Layout

| Path | Role |
|------|------|
| `awesome-cv.cls` | Document class (layout, macros, fonts, icons). Prefer changing content in examples before editing the class. |
| `examples/resume.tex`, `examples/cv.tex`, `examples/coverletter.tex` | Main entry files; set `\documentclass`, `\geometry`, colors, and `\name`/contact macros. |
| `examples/resume/*.tex`, `examples/cv/*.tex` | Section bodies included via `\input{resume/...}` or `\input{cv/...}` from the matching main file. |
| `examples/awesome-cv.cls` | Copy kept alongside examples (may mirror the root class; confirm which file your build resolves). |
| `Makefile` | Builds example PDFs from the repo root. |
| `.github/workflows/main.yml` | CI: compiles with `make` inside `texlive/texlive:latest`. |

## Build and verify

- **From repo root (matches CI):** `make` — produces `examples/resume.pdf`, `examples/cv.pdf`, `examples/coverletter.pdf` using **LuaLaTeX** (`lualatex`).
- **Single file (common locally):** `lualatex -output-directory=examples examples/resume.tex` (run from repo root so `awesome-cv.cls` in the root is found).
- The README also documents **XeLaTeX** (`xelatex ...`). The class uses `fontspec` / `unicode-math`; **pdfLaTeX is not appropriate** for this template.

**Fonts:** CI installs `fonts-roboto` and `fonts-adobe-sourcesans3`. A full TeX Live–style install plus those fonts is enough for local builds.

**Clean:** `make clean` removes `examples/*.pdf` (not auxiliary files like `.aux` / `.log`; those are partly covered by `.gitignore`).

## Editing conventions

- Source encoding: **UTF-8**. Example mains may include `%!TEX TS-program` magic comments for editors; **CI uses the Makefile’s engine**, not those comments.
- Content changes usually go in **`examples/resume/`** or **`examples/cv/`** fragments, not only in the top-level `*.tex` unless you are adjusting global style or personal header fields.
- After structural edits to the class or packages, run `make` and fix LaTeX errors/warnings that affect output.

## CI and quality gates

- **Compile PDFs** (`main.yml`): runs on push and PR; must pass `make`.
- **Integration** (`integration.yaml`): YAML lint on `**/*.{yaml,yml}` when those files change.

## What not to assume

- There is no Node/Python test suite; validation is **LaTeX compilation**.
- Generated artifacts (`*.pdf`, `*.synctex.gz`, aux logs) should not be committed unless the project explicitly tracks them — check `git status` before commits.

## Useful references

- Upstream project: [posquit0/Awesome-CV](https://github.com/posquit0/Awesome-CV)
- Class options and macros are documented in comments inside `awesome-cv.cls` and the example `*.tex` files.
