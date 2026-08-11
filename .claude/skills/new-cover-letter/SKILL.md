---
name: new-cover-letter
description: Create a tailored cover letter PDF for a job position using the Awesome-CV template and save it to cover-letters/. Use when the user gives a job posting (URL or text) and wants a cover letter built and compiled to PDF for this project.
---

# New Cover Letter

Generate a one-page, tailored cover letter PDF from a job posting, matching the existing Awesome-CV style, and save it to `cover-letters/`.

## Inputs
- A job posting: URL or pasted text. If a URL, fetch it. Extract: **exact job title**, company, team, key responsibilities, required skills, and any mission/values.
- If the posting is thin (only title/benefits), note that and keep the letter to a solid generalist angle for that role type — don't invent specifics.

## Steps

1. **Gather the role.** Fetch/read the posting. Pull the exact title (use it verbatim in `\lettertitle`), company name + location (for `\recipient`), and 3–6 concrete requirements to target.

2. **Gather the candidate's real experience.** Read the résumé source — it is the source of truth:
   - `examples/resume/summary.tex`
   - `examples/resume/experience.tex`
   - `examples/resume/skills.tex`
   Use only facts found there (companies, metrics, tech). Do not fabricate achievements or numbers.

3. **Copy the reference letter.** Use `cover-letters/sygnum-cover-letter.tex` as the template. Create `cover-letters/<company>-cover-letter.tex` (lowercase, hyphenated company slug).

4. **Edit the header block.** Keep `\name`, `\mobile`, `\email`, `\homepage`, `\github`, `\linkedin`, `\colorlet`, and footer **verbatim**. Change only:
   - `\recipient{<Company> Recruitment Team}{<Company>\\<Location>}`
   - `\lettertitle{Application for <exact job title>}`
   - `\letteropening{Dear <Company> Hiring Team,}`

5. **Write the three sections.** Same structure as the reference: `About Me`, `Why <Company>?`, `Why Me?`.
   - **About Me:** who Spas is (Software Engineering Lead, 7+ yrs) + the single most relevant proof point for *this* role, tied to the job title.
   - **Why <Company>?:** connect the company's actual mission/problem (from the posting) to what Spas wants to work on. Specific, not flattery.
   - **Why Me?:** map his concrete stack/experience onto the role's requirements. Name the technologies the posting asks for that he genuinely has.
   - Keep it to **one page**. Tight, concrete, no filler.

6. **Sanitize the LaTeX.** ASCII only. No stray Unicode/CJK characters. Escape `&`→`\&`, `%`→`\%`, `#`→`\#`, `_`→`\_`.

7. **Compile with xelatex** (class file is one dir up):
   ```bash
   cd cover-letters
   TEXINPUTS=..:: xelatex -interaction=nonstopmode <company>-cover-letter.tex
   ```
   Confirm the log ends with `Output written on <company>-cover-letter.pdf (1 page)`. If it's 2 pages, trim the body and recompile.

8. **Clean up** build artifacts:
   ```bash
   rm -f <company>-cover-letter.aux <company>-cover-letter.log <company>-cover-letter.out
   ```

9. **Report** the output path and a 1-line summary of the angle taken. Flag if the posting lacked detail.

## Checklist
- [ ] Title in `\lettertitle` matches the posting exactly
- [ ] Recipient company + location correct
- [ ] Every claim traces back to `examples/resume/*.tex`
- [ ] ASCII-clean, special chars escaped
- [ ] Compiles to a **1-page** PDF with xelatex
- [ ] `.tex` + `.pdf` both in `cover-letters/`, aux files removed
