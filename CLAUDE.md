# CLAUDE.md - career-management

Project-specific guidance for Claude Code. User-level rules load automatically; this file
holds only what is specific to this project.

## What this is

A career management app for Australian contractors (starting with Brisbane IT contractors).
It helps you find contract jobs, decide which are worth applying for, write tailored
applications without starting from scratch each time, and track the whole process in one
place. Candidate-first: it works for the job seeker, never for agencies or employers.

## Current stage

**Problem and product definition only.** No technology, architecture, or design has been
chosen yet. The single source of truth for our thinking is
[_docs/01-problem-and-product-definition.md](_docs/01-problem-and-product-definition.md),
which records the problem, the decisions made so far (D1 to D18), the big bets (R1 to R3),
and the principles every decision must pass.

Do not start scaffolding, choosing a stack, or writing app code until a prototype has been
approved (per the user's prototype-before-build rule).

## Non-negotiables (product decisions, do not drift from these)

- **Candidate-first.** The app works for the job seeker, never for agencies or employers.
- **No invented numbers.** Every figure shown (pay, benchmarks) comes from real data seen in
  job ads. If there isn't enough, say so. Never fabricate.
- **Private notes are private forever.** Honest reflections are never shared, never shown to
  agencies or employers, never fed into anything that touches other users.
- **Never reject a winnable job on a guess.** When unsure, show amber and "please check", not
  a silent no.
- **Aim over volume.** Help the user apply to fewer, better jobs, not fire off more.
- **Plain English.** This user is a non-technical founder who is learning. Explain before
  changing anything non-trivial, and write docs in plain English (AU English, no em dashes).

## Layout

- `_docs/` holds all strategic and product docs.
- `README.md` is the short public front door.

## Ports

No dev-server port claimed yet (no app exists). Claim the next free port from
`C:\dev\playbook\projects.md` when the build starts, and record it here.
