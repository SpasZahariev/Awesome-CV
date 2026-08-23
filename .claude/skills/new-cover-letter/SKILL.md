---
name: new-cover-letter
description: Create a concise, evidence-led cover letter for a software engineering role, tailored to the job and company, then compile it with the project's Awesome-CV template. Use when the user provides a job posting or target role and wants a new cover letter in cover-letters/.
---

# New Cover Letter

Create a one-page cover letter that meets the quality bar for senior software engineering applications at FAANG-caliber companies. Make a focused case for fit using verified product and engineering results, not a biography or a list of technologies.

## Required output

- `cover-letters/<company>-cover-letter.tex`
- `cover-letters/<company>-cover-letter.pdf`
- No `.aux`, `.log`, or `.out` files
- A one-page PDF compiled with XeLaTeX

## Evidence rules

Treat candidate claims as a correctness constraint.

1. Read the relevant job posting. If given a URL, retrieve the full posting and distinguish job requirements from generic company material.
2. Read the candidate source of truth:
   - `examples/resume/summary.tex`
   - `examples/resume/experience.tex`
   - `examples/resume/skills.tex`
   - Other `examples/resume/*.tex` files when relevant
3. User-provided facts may supplement the resume. Existing cover letters are style references and leads, not authoritative evidence for new claims.
4. Never invent or inflate metrics, scope, ownership, customers, technologies, motivations, or company facts. Do not turn team results into sole personal ownership unless the source supports it.
5. If a missing fact is essential, ask one targeted question. Otherwise write the strongest truthful letter from available evidence.

## Build the role-fit brief

Before drafting, extract a compact internal brief:

- Exact job title, company, team, location, and requisition ID if present
- The product or customer problem the team owns
- Three to five highest-signal requirements
- Expected level signals: scope, system design, execution, collaboration, leadership, or domain depth
- One or two specific reasons this company or team is a credible match
- The two or three candidate achievements that best prove fit

Prioritize requirements that are repeated, described as core responsibilities, or tied to the team's product. Separate hard requirements from optional keywords. Do not try to mention every item in the posting.

For senior and lead roles, favor evidence of:

- Measurable product, customer, operational, or business outcomes
- Scale, latency, reliability, correctness, security, or cost improvements
- Architecture and production ownership
- Ambiguous problem solving and sound technical judgment
- Cross-team influence, mentoring, or engineering leadership

## Write impact-first evidence

Use the Google-style XYZ pattern as a reasoning tool:

> Accomplished X, measured by Y, by doing Z.

In natural cover-letter prose, usually order the sentence as:

1. Result or user value
2. Quantified scale or measurement
3. Technical action and relevant context

Strong examples from the current resume:

- Cut messaging turnaround by about 85%, from 30 minutes to under 5 minutes at 150K+ messages per hour, by redesigning a Java service around Kafka and asynchronous processing.
- Scaled regulatory data reconciliation to 500K+ entities per day across 12 source databases by designing a cloud ingestion and transformation workflow and leading a seven-engineer team.

Do not force the formula into every sentence. Use qualitative outcomes when no honest metric exists, but still state who benefited, what changed, and how the candidate contributed. Prefer two developed achievements over five shallow claims.

## Drafting standard

Write for a recruiter or hiring manager scanning the letter in under a minute.

- Usually target 250 to 400 words, then shorten further if needed for one page.
- Open with the exact role, the candidate's relevant positioning, and the strongest proof point. Avoid generic openings.
- Connect company interest to a concrete product, engineering challenge, customer problem, or mission found in the posting or an authoritative company source.
- Show why the candidate's past results predict success in this role. Translate experience into the employer's needs rather than repeating resume bullets.
- Include role keywords naturally where supported by evidence. Do not keyword-stuff or dump the full technology stack.
- Close with the specific contribution the candidate can make. Keep the closing confident and brief.

Use two or three short `\lettersection` sections. The default structure is:

1. `Why Me?` or `About Me` - positioning plus the strongest role-relevant result
2. `Why <Company>?` - a specific and credible connection to the team's work
3. Optional second evidence section when needed to prove technical breadth, leadership, or domain fit

The section order may change when a stronger narrative results. `About Me` must not become a career summary.

## Reject weak language

Remove:

- Generic praise that could be sent to any company
- Claims such as "perfect fit", "dream company", "passionate", or "world-class" without evidence
- Resume chronology, long skill inventories, and copied job-description language
- Unsupported superlatives and exaggerated ownership
- Empty soft-skill claims such as "team player" or "fast learner"
- Repeated facts, throat-clearing, and sentences that do not improve the hiring case
- Overly ornate prose, buzzwords, and obvious AI-generated phrasing

Prefer direct verbs, concrete nouns, short paragraphs, and varied sentence structure. Sound like an experienced engineer: precise, credible, product-aware, and technically fluent.

## Create the LaTeX file

1. Use `cover-letters/sygnum-cover-letter.tex` as the default structural template unless the user identifies another approved letter.
2. Create `cover-letters/<company>-cover-letter.tex`, using a lowercase hyphenated company slug.
3. Copy the contact block, color configuration, closing, and footer verbatim from the selected template.
4. Change only the role-specific fields and body unless layout changes are required to preserve a polished one-page result:
   - `\recipient`
   - `\lettertitle`
   - `\letteropening`
   - `\lettersection` headings and content
5. Use the exact posting title in `\lettertitle`. Include a requisition ID only when useful.
6. Use ASCII in `.tex` body content. Escape LaTeX special characters, including `\&`, `\%`, `\#`, and `\_`.

## Compile and inspect

Compile from `cover-letters/` so the root-level class is available:

```bash
TEXINPUTS=..:: xelatex -interaction=nonstopmode <company>-cover-letter.tex
```

Verify:

- XeLaTeX exits successfully
- The log reports a one-page PDF
- No overfull boxes, missing characters, broken URLs, or obvious warnings affect the result
- The rendered PDF has balanced spacing, no clipped text, and no nearly empty trailing section

If the PDF is two pages, improve the writing before changing layout: remove repetition, compress weaker evidence, and shorten the company paragraph. Do not solve poor editing with tiny fonts or cramped margins.

Clean build artifacts:

```bash
rm -f <company>-cover-letter.aux <company>-cover-letter.log <company>-cover-letter.out
```

## Final review

- [ ] Exact company, title, team, location, and requisition details are correct
- [ ] Opening contains a strong result, not a generic introduction
- [ ] Two or three achievements directly address the role's highest-signal needs
- [ ] Impact statements lead with outcomes and include honest measurements where available
- [ ] Seniority is demonstrated through scope and results, not asserted through adjectives
- [ ] Company motivation is specific, accurate, and not flattery
- [ ] Every candidate and company claim is traceable to a source
- [ ] The letter complements rather than restates the resume
- [ ] `.tex` is ASCII-clean and LaTeX special characters are escaped
- [ ] PDF is polished and exactly one page
- [ ] `.tex` and `.pdf` are in `cover-letters/`; temporary files are removed

Report the two output paths and one sentence describing the chosen hiring case. Flag any important posting detail that could not be verified.
