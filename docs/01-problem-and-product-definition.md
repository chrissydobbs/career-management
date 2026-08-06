# Career Management Platform — Problem & Product Definition

> **Status:** Living document. This is *thinking made concrete*, not a spec.
> No technology, architecture, or implementation decisions are captured here yet — by design.
> **Last updated:** 2026-08-06

---

## Decisions log

Founder decisions made explicitly. These are settled unless revisited here.

| # | Decision | Choice | Date |
|---|----------|--------|------|
| D1 | **Decision surface** — how "worth applying or not" is shown | **Traffic light + one plain-English reason** (e.g. "NV1 required — you don't hold it"). Fast, trustable, low cognitive load. | 2026-08-06 |
| D2 | **Getting jobs into the system at launch** | **A mix:** manual paste-link / forward-email as the reliable floor, plus browser-extension capture and best-effort aggregation layered on where they work. Product must stay valuable on the manual floor alone. | 2026-08-06 |
| D3 | **MVP heart — what we design & build first** | **The tracker / spine** — the append-only memory of every role, action, agent and outcome. Useful even with manual entry; makes every other box stop starting from scratch. | 2026-08-06 |
| D4 | **Monetisation** | **Undecided — deliberately open.** Revisit once the wedge and value are proven; design so it doesn't foreclose candidate-subscription *or* hiring-side options. | 2026-08-06 |
| D5 | **Day-one 'red' rules** | The four hard filters, all active: (1) rate below floor, (2) eligibility not met, (3) wrong location / unacceptable onsite, (4) already seen (duplicate). See §7a. | 2026-08-06 |
| D6 | **Capture model** | **Extraction-first.** User pastes a link / forwards an email; system extracts title, client, rate, ref, closing date; user only corrects. → *Parsing quality is a first-order requirement, not a nicety.* | 2026-08-06 |

---

## 0. How to read this document

This is the shared brain for the product. It captures **what problem we're solving, for whom, and why** — grounded in the founder's own lived experience as an Australian government IT contractor, not in a market report.

It deliberately stops *before* features, UI, and technology. When we start designing screens and systems, they must trace back to something written here. If a proposed feature doesn't serve a problem on this page, it doesn't belong.

Everything here is provisional and meant to be argued with. Open questions are tracked in §9.

---

## 1. The problem, in one paragraph

Managing a career in Australia is fragmented, repetitive, and demoralising. The same information is re-entered across SEEK, LinkedIn, recruiters, and government portals. Every role demands a bespoke resume and suitability statement, written from scratch, at the moment you know the least about whether it's worth writing — and then sent into a void that almost never replies. The candidate is the least-informed, least-powerful party in every interaction, and the system quietly trains people to give up.

## 2. The real problem (not the obvious one)

The obvious framing is **time and friction** — too much re-typing, too many platforms. That's real, but it's the symptom. Building against it produces a slightly better resume-builder in a crowded, commoditising market.

Two deeper problems sit underneath:

1. **Total information and power asymmetry.** The candidate never knows what a role really pays, whether it's genuinely open, whether the recruiter is working for them, whether the offer is good, or what their next move should be. The re-typing is annoying; **deciding blind is what costs people years and tens of thousands of dollars.**
2. **High-stakes, low-frequency decisions made without a coach.** People make ~8–12 consequential career moves in a lifetime, each under stress, each with no trusted advisor who knows *both them and the market.* The wealthy have mentors and executive coaches. Everyone else has a mate's opinion and a Google search.

### The villain, named precisely

The pain is not "time." It is:

> **effort × uncertainty × no-feedback**

You spend your most expensive effort (a bespoke suitability statement) at the point of *least* information, and get *nothing* back to tell you whether it mattered. That loop — high sunk cost per shot into a feedback-free void, repeated until the energy is gone — is the machine that produces burnout. **Every product decision is measured against whether it shrinks one of those three terms.**

## 3. Who this is for (the wedge)

**Australian professional contractors — starting with Queensland / government ICT contractors.**

This is chosen deliberately, from the founder's own scars, over a broad horizontal "everyone" launch:

- **Recurring, acute pain** — a new contract every 6–12 months, forever.
- **Real money** — day rates high enough that saved time and better rate negotiation pay for the product.
- **Quantifiable value** — "you're 8% under market," "don't waste a statement on this one."
- **Naturally recurring engagement** — extensions and re-contracting keep the tool warm (the retention problem that kills most career products).
- **Deeply underserved** — global tools get none of the Australian/government specifics right.

Horizontal ("perm, grads, execs, career-changers, consistent experience for all") remains the **long-term platform vision** — but it is a dangerous *starting* strategy. Win this wedge completely first.

### Australia-specific texture that changes the product

- **Total remuneration is genuinely hard to compare** — "package including super" vs "plus super" (super is 12% from July 2025), salary packaging, NFP/health caps, novated leases, FBT.
- **The contractor economy** — day rates, agency margins, ABN vs PAYG (`$100/hr + super PAYG` vs `$112/hr + GST ABN`), extensions, PSI rules.
- **Government as its own genre** — APS/state levels, merit selection, addressing selection criteria, capability frameworks, and **security clearances** (Baseline/NV1/NV2) as a first-class eligibility filter.
- **Authority to Represent & double-submission** — you can be represented by only one agency per role reference number; being submitted twice can disqualify you.
- **Working rights / visa status** as a primary hiring filter.
- **Professional registration & clearances** as hard, verifiable eligibility facts.
- **Tall-poppy culture** — Australians are culturally uncomfortable self-promoting, which makes resumes, LinkedIn, and interview self-advocacy genuinely harder. Helping people advocate authentically (not American hype) is a real angle.

## 4. The founder's lived workflow (the ground truth)

The exact loop this product exists to break, as lived:

1. **Doom-scroll** SEEK / LinkedIn / SmartJobs. Hours. Terrible UIs. The same role appears under three agencies.
2. **One-click "apply."** This is *theatre* — an expression of interest dumped to an agent's inbox. ATS may or may not parse you. A human may or may not look. **Zero feedback.**
3. **The agent bites (or doesn't).** If they do, an email arrives (see the RoadTek / ref `1651209` example): *now* send an updated resume in Word, *now* write a 1–2 page suitability statement against the JD, *now* sign the Consent Form and **Authority to Represent** via Dochub — "once shortlisted."
4. **Hours spent** compiling a bespoke pack for *this* role.
5. **Sent into the void.** Silence, unless you're one of the few selected for interview.
6. **Repeat, thousands of times, until the energy is gone.**

Two facts from the founder that shaped everything below:

- **On tailoring:** *"I upload my CV, the JD, the criteria, and ask AI to write it — then iterate 50 million times."* → The villain is **statelessness**. The AI has no memory of you or your last 400 statements, so you re-teach it your voice every single time.
- **On ghost roles:** *"I've never thought about whether a role is real — is there a way to tell?"* → If a veteran of thousands of applications can't tell, **no individual can.** The asymmetry is total. That's not naivety; it's the market gap.

## 5. The core insight: the thread *is* the product

Every individual box already exists as a standalone product — job search, CV tailorer, tracker, interview-prep generator. **None of them talk to each other, or to a memory of you.** What doesn't exist is the *continuity* between them.

This is explicitly **not** "another CV/LinkedIn optimiser." It is the **end-to-end process**, connected by a spine of memory.

### The flywheel

```
Search → Score → Tailor → Track → Interview → Outcome
   ↑                                              │
   └──────────  feeds back into  ─────────────────┘
        (Score & the career profile get smarter)
```

Every action leaves a residue that makes the next cycle cheaper and smarter:

- The role you tracked teaches the scorer which agencies and role-types actually convert **for you**.
- The statement you tailored (with your input) enriches your profile, so the next one drafts closer to your voice — iteration count *falls over time*.
- The outcome you record — interview, ghost, "this agent is useless" — is the signal the open market denies you, and it sharpens "worth applying or not" for every future role.

**The moat is the accumulating memory, not the generation.** CV generation is commoditising to zero. Search is the incumbents' most-defended asset. The defensible core is the memory that makes cycle 400 cost a fraction of cycle 1 and land better.

### The product philosophy fork (decided)

Cheaper applications must **not** quietly become "apply to more." The fix for burnout is **cheaper effort + a real feedback loop, aimed at fewer, better-chosen roles.** A product brave enough to say *"apply to none of these today"* is the one that gives the user their energy back. **Targeting and quality over volume and speed.**

## 6. The spine — the data model of a career

The spine is the heart. Item 2 ("is it worth applying?") is not a feature you build — it is a **function computed over the spine's data**:

> `score = f( what the spine knows about YOU × what it knows about THIS ROLE × what it has learned from every role before )`

**Discipline:** every piece of data earns its place only if it feeds **fit, winnability, tailoring, or reflection.** If it feeds none, cut it.

The spine has two halves that stay separate, plus a derived layer.

### Half A — the durable "You" (changes slowly, outlives every job)

The single source of truth. Roles churn; this accumulates.

- **Eligibility facts** — location/SEQ, working rights/visa/citizenship, security clearance (Baseline/NV1/NV2), professional registrations, notice period/availability, PAYG vs ABN setup. These are **hard filters** — a role needing NV1 you don't hold is unwinnable instantly. Cheap, binary, first gate.
- **Engagement preferences** — perm vs contract, rate floor, locations/remote, industries, role types, deal-breakers. Defines "does this even fit my criteria."
- **Evidence atoms** — *the single most important modelling decision.* Not a master-resume blob, but granular, reusable, tagged achievements ("led in-vehicle telematics rollout across X vehicles, delivered Y"), tagged by skill/capability/domain/seniority. A suitability statement becomes *select the right atoms + frame them against the JD.* **Crucially, the user does not enter atoms by hand — nobody thinks that way.** The system *extracts and remembers* them from uploaded CVs, tailored JDs, and accepted/rejected iterations. This is what makes cycle 400 cheap.
- **Skills & capabilities (normalised)** — so roles can be matched to you, ideally aligned to how government describes capabilities.

### Half B — the "Role" lifecycle record (one per opportunity, churns constantly)

The tracker's core unit.

- **Primary key = reference number.** `1651209` collapses the same RoadTek role — appearing via Hays *and* Peoplebank *and* SmartJobs — into **one** record. Without this the tracker is noise and double-submission risk is invisible. *(Fallback dedupe for LinkedIn / private roles with no ref number: title + client + rate + JD similarity. Don't over-fit the spine to government.)*
- **Role identity** — ref, title, client, source(s), JD text, rate, duration, location, closing date, requirements.
- **Agency touches (many per role)** — which agent, when, how, what they asked for, and **who holds Authority to Represent** for this ref.
- **Your actions** — applied where/when, which pack versions produced and sent, forms signed.
- **Responses & outcomes** — replied / ghosted / shortlisted / interview / offer / rejection, each timestamped.
- **Reflections** — agent quality, interview notes, "didn't like this person," "what I'd do better." **The crown jewel** — recorded nowhere else on earth, un-scrapeable, and what makes the system genuinely *know* you.
- **The score + its reasons at decision time** — so we can later check whether the score was right, and learn.

### The rule tying both halves together: timeline, not status

Do **not** model a role as `status = rejected`. Model it as an **append-only event log**: applied Tuesday → agent emailed Thursday → sent pack Friday → silence → rejected three weeks later. Because:

1. It reconstructs context when an agent surfaces weeks later (the "which role was this again?" problem).
2. The *sequence and timing* is the raw material for learning what a ghost role's lifecycle looks like.

### Two capture modes, everywhere

- **Auto** — populated from the user's own actions (generated a pack, clicked apply).
- **Manual overlay** — the things the system can't see: an agent's phone call, interview feedback, reflections. This is the **highest-value data and must be frictionless to add** (e.g. a voice note after an interview).

## 7. The derived layer — this *is* "item 2"

Nothing here is stored; it is all computed from A × B × history.

**Fit** (cheap, works day one, needs only *your* data): eligibility hard-filters → skill/capability overlap → seniority → rate acceptable → location. Fails fast on hard filters.

**Winnability** (the valuable part, learned from Half B accumulating over time):

- **Duplicate?** — have I already seen/applied to this? (ref-number dedupe)
- **Ghost / compliance smell:**
  - *Visible to you alone, if tracked:* same ref/JD reappearing every few weeks; rolling/extending closing dates; the same role sprayed via 5 agencies at once; an agency that always asks for your pack then ghosts (candidate-database building, not a live vacancy).
  - *Only visible with accumulated data:* this agency/client/role-type has a submission→interview rate near zero — a statistical black hole invisible from a single posting.
- **Agency conversion history** — does *this* agent ever actually progress me? (straight from my outcome log)
- **Rate** vs my floor and vs market.
- **Staleness / competition** — how long open.

**Effort-vs-reward** — given predicted winnability and whether I can reuse atoms or must write fresh, is it worth my energy? This is where the product is brave enough to say *"apply to none of these today."*

## 7a. The minimum role record & the day-one traffic light (resolves Q6)

Because we build the spine first (D3) with extraction-first capture (D6) and a traffic-light surface (D1), the question is: **what is the smallest role record that is cheap to capture yet already powers a useful red/amber/green on day one?**

### The red rules are personal, set at onboarding

The four hard filters (D5) are **not hardcoded** — they are the user's own criteria, **selected during onboarding and editable anytime.** Each user's traffic light is calibrated to *their* floor, *their* eligibility, *their* locations. This is what lets one consistent surface adapt to every individual (the long-term platform promise, delivered cheaply from the start).

Onboarding therefore captures, once, the Half-A facts that drive the day-one light:

- **Rate floor** (with PAYG+super vs ABN+GST understood).
- **Eligibility held** — clearance level, working rights/citizenship, key registrations.
- **Location / onsite tolerance.**
- **Deal-breakers** — the red rules the user switches on.

### Trust tiers — not all reasons are trusted equally

A crucial nuance from the founder: a reason being a *deal-breaker* is **not** the same as *trusting the system's call on it*. The founder marked all four as deal-breakers, but would only skip *without second-guessing* on the **objective, checkable** ones.

- **Tier 1 — auto-trust (may firmly red or even silently filter):** *rate below floor*, *duplicate / already-seen*. Objective, verifiable, no judgement required.
- **Tier 2 — show but let the user verify / override (never silent-filter):** *eligibility mismatch* (users trust their own read on eligibility), *agency track record* (inferred, cold-start, small sample — low trust until proven).

**Design implication:** Tier 1 reasons can drive confident reds and are the safest thing to build first. Tier 2 reasons appear as context/amber with a "here's why, you decide" framing — earning trust over time rather than assuming it. This maps directly onto the cold-start truth in §8.

### Minimum role record for a day-one light

Enough to evaluate the Tier-1 rules and reconstruct context later:

- **Reference number** (or fallback key: title + client + rate + JD similarity) — powers *duplicate* detection.
- **Rate** (and PAYG/ABN basis) — powers *rate below floor*.
- **Title, client, source, closing date** — context + the "which role was this again?" fix.
- **JD text** (captured, not hand-typed) — feeds later fit/tailoring; not required for the day-one light.

Everything beyond this is enrichment. The light works from ref + rate + the user's onboarding criteria — all of which extraction-first capture can populate with almost no typing.

### Founder profile (test user #0) — and a wedge refinement

Seeded facts from the founder, who is the first real user:

- **Clearance: none.** → Any role requiring Baseline/NV1/NV2 is an instant eligibility red for this user. **This sharpens the wedge:** the founder's realistic pool is **Queensland *state* government + private-sector SEQ contracts** (e.g. RoadTek/TMR-style transport roles that don't require federal clearance), **not** federal/defence/Canberra-cleared work. Worth remembering when we reason about the beachhead — "government contractor" is really "state-government + private contractor" for this user.
- **Capture tolerance: almost nothing typed** — reinforces D6.
- **Rate floor: TBD** — to capture at onboarding.

## 8. The cold-start sequencing truth

The product does **not** launch omniscient:

- **Fit scoring works day one** — it needs only the user's own data.
- **Stateful tailoring** and the **tracker** (ending "which role was this again?") deliver value immediately.
- **Winnability / ghost detection has a cold start** — weak with one user and no history; it *grows* as the user's own tracker fills, then *compounds* as more users join (a genuine data network effect no lone competitor can hand a new user on day one).

This is a feature, not a flaw. Early users who let the system accumulate their history get something late competitors can't replicate.

## 9. Open questions (actively unresolved)

1. ~~**The decision surface**~~ — **Resolved (D1):** traffic light + one plain-English reason. Still open *underneath*: exactly which reasons we can generate on day one vs later.
2. **Who pays, and when** — **Held open (D4).** Candidate subscription (aligned, intermittent willingness-to-pay) vs hiring-side money later (bigger, but tension with "we work only for you"). Design so neither door is foreclosed.
3. ~~**Unified search feasibility**~~ — **Direction set (D2):** manual paste/forward is the reliable floor; extension + best-effort aggregation layered on. Still open: how good the paste/forward parsing has to be to feel effortless.
4. **Reflection capture UX** — how to make the crown-jewel subjective data effortless to record in the emotional moment right after an interview.
5. **Motivation & dignity as design requirements** — the product does psychological work, not just functional. How does "this took 4 minutes and is building into something" replace "this took 3 hours and vanished"?
6. ~~**The spine's decision surface**~~ — **Resolved (§7a):** minimum record = ref + rate + title/client/source/closing (+ JD text captured); red rules are personal and set at onboarding; reasons have trust tiers. Still open underneath: how good extraction has to be to feel effortless (ties to Q3-underneath).
7. **Rate floor & onboarding set** *(new)* — the founder's rate floor is still TBD; more broadly, what exactly does the onboarding flow capture, once, to calibrate the day-one traffic light without feeling like a chore?

## 10. Explicitly out of scope (for now)

- Any technology, architecture, or implementation decisions.
- A standalone "optimise my CV / LinkedIn" tool — that already exists and is commoditising; we build the *end-to-end thread*, not another point solution.
- Horizontal launch across all user types simultaneously — deferred until the contractor wedge is won.
- Employer/recruiter-side product — candidate-first; revisit only with eyes open on the conflict it introduces.

---

## Core principles (the test every decision must pass)

1. Shrink **effort × uncertainty × no-feedback** — the named villain.
2. **The thread is the product** — continuity and memory, not any single box.
3. **The moat is accumulating memory**, not generation or search.
4. **Targeting and quality over volume and speed** — help make better decisions, not submit more applications.
5. **Be brave enough to say "don't apply."**
6. **The user should never re-enter what the system already knows** — capture passively; manual entry only for what can't be seen, and make even that frictionless.
7. **Win the Australian contractor wedge completely before generalising.**
