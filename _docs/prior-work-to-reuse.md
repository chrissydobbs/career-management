# Prior work we can reuse

> A reference note, not a plan. It records what already exists in earlier projects so we don't
> rebuild from scratch when the time comes.
> **Written:** 2026-08-07

There are **two** earlier resume projects, both worth mining. career-management does not merge
their code. They are **donors**: we take the valuable, mostly stack-independent parts (your
real data, your voice rules, the "select don't invent" approach, the proven output) and leave
the apps behind.

- **`resume-builder`** (`C:\dev\resume-builder\`, June 2026) is the **more advanced and more
  recent** one. Start here.
- **`automated-cv-builder`** / "JobReady" (`C:\dev\automated-cv-builder\`, April 2026) is the
  predecessor. Useful for a few things resume-builder doesn't have (job scraping, a tracker).

## The single most important thing both projects prove

Both landed on the same hard-won principle, and resume-builder makes it a locked, tested rule:

> **The AI selects from content that already exists. It never invents text, never rewrites
> bullets. Every claim must trace back to real CV content.**

This is exactly career-management's principle "rules decide, the AI doesn't fabricate." It is
not a theory here, it is working code with tests. That is a strong signal we're right, and a
ready-made pattern to reuse.

## resume-builder (the primary donor)

| Asset | Where it lives | What it gives career-management |
|---|---|---|
| **Most evolved content model** | `resume-content.json` | A "library plus selected" structure: a library of reusable profile paragraphs, career highlights, competencies and skills, and the chosen set. This is the "achievements in small pieces" idea in its most developed form. Seeds the memory. |
| **Voice as a machine-readable rules file** | `rules.md` | One file that is the single source of truth for banned characters (em dashes), banned words, locked sections, and style. Both the AI prompts and the code checker read it. Directly reusable as the seed for "sounds like you". |
| **A tested compliance layer** | `src/compliance/` (`deterministic.js`, `rules.js`, `deterministic.test.js`) | Two-layer checking: a deterministic code check (parses the banned lists from `rules.md`) plus an LLM check, with failures routed back and retried up to 3 times. This is voice and anti-fabrication enforcement done properly, with tests. |
| **A working five-stage AI pipeline** | `src/pipeline/` (`intake`, `analyst`, `tailor-cv`, `cover-letter`, `compliance-agent`, `run`) | intake a JD, pick a CV variant and keywords, tailor only the summary and skills, write a cover letter, then check compliance. A proven architecture for the writing slice. |
| **Clean output approach** | `docxtemplater` + a Word base template, plus an HTML render (`src/templates/resume.html.njk`, `src/render.js`) | Visual design is edited in Word, not code. Cleaner than building the doc programmatically. |
| **Writing reference** | `source_docs/writing_reference.md` | The tone reference the agents follow. |

## automated-cv-builder / JobReady (the predecessor donor)

| Asset | Where it lives | What it gives career-management |
|---|---|---|
| **A working SEEK scraper** | `lib/scraper.ts` | Playwright selectors that work. For when we go past paste-and-forward capture (which is deliberately later, because scraping is fragile). |
| **A tracker and data models** | `_docs/product-brief.md` (jobs, applications, generated_docs, user_profile) | resume-builder has no tracker; JobReady does. A starting point for the tracker's shape. Note: it uses a simple status field; we decided on a running timeline, so the model evolves, it isn't copied. |
| **A full product brief** | `_docs/product-brief.md` | The end-to-end workflow, MVP scope, and Claude prompt patterns written up. Lots of overlapping thinking. |
| **Earlier master data** | `resume_build/resume_master.json`, `WRITING_RULES.md`, `RESUME_RULES.md` | An earlier version of the content and voice rules. resume-builder's versions are newer, but this is worth diffing for anything lost between versions. |

## Honest caveats

- **Stack mismatch.** Both are Next.js apps. The playbook default is React 19 + TanStack + Vite
  + Supabase. So the *code* likely won't port cleanly, but the *data, rules, compliance logic,
  pipeline design and output approach* will.
- **Lots of overlapping iterations.** Three projects circling the same problem, and JobReady
  alone has eleven `build_resume_v2..v11.js` files. Take the current, canonical versions
  (resume-builder's pipeline and `resume-content.json`), not the pile.
- **Content is hand-written.** The libraries were authored by hand. career-management wants them
  collected automatically, but the hand-written libraries are perfect seed material.

## Security check (done 2026-08-07)

Both projects' secret files are safe: `automated-cv-builder/.env.local` and `resume-builder/.env`
were each never committed, never pushed, and are properly gitignored. Only the `.env.example`
files are tracked. Nothing exposed, nothing to rotate.

## A registry discrepancy to flag (not fixed here)

`resume-builder` is **not listed in `projects.md`**, and its `CLAUDE.md` claims **port 8086**,
which `projects.md` assigns to `chrissydobbs.ai`. So there is a port clash and a missing entry
in the registry. Worth tidying separately when the projects list gets a review.

## Recommendation

When we start building career-management's first slice, harvest in this order:

1. From **resume-builder**: the content model (`resume-content.json`), the voice rules
   (`rules.md`), the tested compliance layer (`src/compliance/`), and the pipeline design.
2. From **JobReady**: the SEEK scraper and the tracker data models, for later slices.
3. Copy into a clearly marked reference folder first, then adapt to career-management's stack
   and its timeline-based data model.

Decide both donor projects' fate (retire or keep parked) once these are safely harvested.
