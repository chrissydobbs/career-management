# What we can reuse from JobReady (automated-cv-builder)

> A reference note, not a plan. It records what already exists in an earlier project so we
> don't rebuild it from scratch when the time comes.
> **Written:** 2026-08-07

## What JobReady is

`automated-cv-builder` (internally called "JobReady") is a working prototype built in April
2026, living at `C:\dev\automated-cv-builder\`. It's a local Next.js app that already does a
good chunk of what career-management wants: scrape jobs from SEEK, show a job board, tailor a
resume and cover letter from a master data file, and track applications.

We are **not** merging its code. It's a **donor**: we take the valuable, stack-independent
parts (your real data, your writing rules, your resume design, the prompt patterns) and leave
the app behind.

## The genuinely reusable assets (and what they seed here)

| Asset in JobReady | Where it lives | What it gives career-management |
|---|---|---|
| **Your career history in reusable pieces** | `resume_build/resume_master.json` (48KB) | The biggest head start. Personal details, positioning paragraphs, competencies, technical skills, 10 roles with bullet variants, certs, education. Seeds the "you" half of the memory, and the "achievements in small pieces" idea, already written and real. |
| **Your voice as hard rules** | `resume_build/WRITING_RULES.md`, `resume_build/RESUME_RULES.md` | No em dashes, a banned-words list (leverage, utilise, seamless, robust), no generic PM phrases, first person, plain English, three-paragraph cover notes. This is the "sounds like you, not a robot" starting point, before the app learns your style automatically. Matches the global writing rules. |
| **A proven resume design and builder** | `resume_build/build_tailored.js`, plus `output/*.docx` | A polished .docx (navy header, Calibri, two-column) that hiring managers have already seen. Five real resumes exist in `output/`. |
| **The right tailoring approach** | `_docs/product-brief.md` (Claude prompt patterns), `build_tailored.js` | The AI *selects* which of your existing pieces fit a job and a script assembles the document. It does not invent content. This is exactly our "rules decide, AI doesn't fabricate" principle, already working. |
| **Real worked examples** | `resume_build/tailor_tmr.json`, `tailor_ghd.json`, `tailor_davidson.json`, etc. | Actual "which pieces for which job" configs for real companies. Good examples of the select-pieces pattern. |
| **A working SEEK scraper** | `lib/scraper.ts` | Playwright selectors that work. For when we go past paste-and-forward capture (which is deliberately later, because scraping is fragile). |
| **Starter data models** | `_docs/product-brief.md` (jobs, applications, generated_docs, user_profile) | A starting point for the tracker's shape. Note: JobReady uses a simple status field; we decided on a running timeline, so the model evolves, it isn't copied. |

## Honest caveats

- **Stack mismatch.** JobReady is Next.js + SQLite + Playwright + docx-js. The playbook default
  is React 19 + TanStack + Vite + Supabase. So the *code* likely won't port cleanly, but the
  *data, rules, prompts and design* will.
- **Atoms are hand-written there.** You wrote the bullet variants by hand. We want them
  collected automatically. But your hand-written master is perfect seed material.
- **Iteration clutter.** There are eleven `build_resume_v2..v11.js` files. Only
  `build_tailored.js` is the real one. Take that, not the pile.
- **Scraping vs capture.** JobReady auto-scrapes SEEK daily. We decided paste/forward first,
  scraping later. The scraper is a bonus, not the base.

## Security check (done 2026-08-07)

JobReady's `.env.local` (which holds a live Anthropic API key) was checked: never committed,
never pushed, properly gitignored. Only `.env.example` is tracked. Nothing exposed, nothing to
rotate.

## Recommendation

When we start building career-management's first slice, copy across (into a clearly marked
reference folder, then adapt):

1. `resume_master.json` as the seed for your profile and achievements.
2. `WRITING_RULES.md` and `RESUME_RULES.md` as the seed for your voice.
3. `build_tailored.js` and the resume design as the proven output format.
4. The Claude prompt patterns from the product brief (select, don't invent).

Leave the rest. Decide JobReady's fate (retire or keep parked) once these are safely harvested.
