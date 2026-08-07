# Scope: what we build, and when (Phase 3)

> Part of the problem-first product build. This is the initial requirements: the first version,
> then v1, then v2, and what we deliberately do not build.
> **Written:** 2026-08-07

The rule for this page: the first version is the smallest thing that proves the edge and gives
you a real reason to use it. Everything else waits. Size is rough build effort: S small, M
medium, L large.

## First version (MVP) — aim: under 4 weeks

**What it proves:** you can stop wasting time on bad jobs, and the app starts remembering you
(the first taste of the core edge).

| Feature | Why it's in | Size |
|---|---|---|
| Quick setup (your criteria) | So there's something to score against: minimum pay (PAYG and ABN), locations and office days, roles you want, absolute no's, eligibility and what you could get | M |
| Capture a job (paste a link or forward an email) | Bring a job in; the app reads out title, client, pay, reference number, closing date. This is the reliable base, not auto-search | M/L |
| Start remembering | Store your criteria and every job you've seen. This is the seed of the memory, and it's what makes the next two work | S |
| Red / amber / green signal, plus one reason | The "worth applying?" answer. Uses the checkable rules: pay below floor, can't-meet eligibility (three states), wrong location, already seen. Unclear clearance shows amber and "please check" | M |
| Spot duplicates | Catch the same job seen before, by reference number or a close match. Powers "already seen" and starts the anti-ghost work | S/M |

**If you had half the time, cut:** the auto-reading (paste the few fields by hand), the reason
text (show colour only), and setup depth (ask two things, not five). Shipping a rougher version
sooner beats a polished one later.

## v1 — the version you'd use daily during a hunt

**What it proves:** the core edge in full. It remembers you, so applications are faster and
sound like you.

| Feature | Why it's in | Size |
|---|---|---|
| Writing help | Tailor a suitability statement and CV in the app, built from your remembered pieces, sounding like you. You and the app together, it selects from what exists and never invents | L |
| The tracker | A running timeline for each job: agency contacts, what you did, responses, outcomes. Keyed on the reference number. Ends "which job was this again?" | L |
| Visible growing profile | Show the chain: your profile grew, that produced an outcome, that saved you time. The anti-burnout engine (D19) | M |
| Build a pack on demand or in advance | Put a full application pack together when you need it | M |

## v2 — once there are real users

**What it proves:** the parts that need accumulated history, more people, or the harder plumbing.

| Feature | Why it waits | Size |
|---|---|---|
| Reflections and interview capture | Needs the interview known (calendar), and it's about depth, not first value | M/L |
| Keep-warm hooks | Contract-end wake-up and the pay-rate drip. Matters once you're a returning user, not on day one | M |
| Ghost-job detection | Needs your history (and later other people's) to be any good | M |
| Build a pack from a forwarded agent email | Nice automation, but the manual pack works first | M/L |
| Better capture | Browser helper and best-effort auto-pulling of jobs. The fragile part the big sites fight hardest | L |
| Cross-user signals | Agency track records at scale. Needs many users | L |
| Owning the government forms | Currently track-only. Filling and signing them is a big, later piece | L |

## What we never build (or not now)

| Not building | Never or not-now | Why |
|---|---|---|
| Inventing numbers | Never | Kills trust the moment you catch it. Real data or "not enough data" |
| Mass-apply / one-click spam to everything | Never | Against the whole philosophy. Fewer, better applications, not more |
| Showing or sharing your private notes | Never | The honesty is the value, and it only exists if they never leave you |
| Hiding a winnable job on a guess | Never | Unclear means amber and "please check", not a silent no |
| A generic standalone CV / LinkedIn tidier | Never | That already exists and is becoming cheap. We build the joined-up thread |
| Building for agencies or employers | Not now (likely never) | We work for the job seeker. Only ever revisited with clear eyes on the conflict |
| Graduates and juniors as a target | Not now | Little history to remember, low ability to pay |
| Non-Australian markets | Not now | Australia only to start |

## Why these cuts are safe

Everything deferred adds cleanly later, because the memory is built first and everything else
sits on top of the same captured data:

- The tracker and the writing help both read the same job records and profile the first version
  already builds.
- Keep-warm hooks and ghost detection just read history that's been accumulating from day one.
- Growing to other user types and markets is mostly more data and settings, not a rebuild.
  **Scalability is a stated requirement** (from Phase 2), so the foundation is built to stretch.

## Exit check

- First version is small enough to aim for under 4 weeks (rough).
- v1 is a clear, bounded set (writing plus tracker).
- v2 is listed but not yet scheduled.
- The "never / not now" list has more than five items, each with a reason.
