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
| D5 | **Day-one 'red' rules** | The four hard filters, all active: (1) rate below floor, (2) eligibility you **cannot** meet, (3) wrong location / unacceptable onsite, (4) already seen (duplicate). **Eligibility is three-state** — hold / can-obtain / can't-meet — and only *can't-meet* is red; "ability to obtain" stays in play. See §7a. | 2026-08-06 |
| D6 | **Capture model** | **Extraction-first.** User pastes a link / forwards an email; system extracts title, client, rate, ref, closing date; user only corrects. → *Parsing quality is a first-order requirement, not a nicety.* | 2026-08-06 |
| D7 | **Onboarding** | **Under 2 minutes**, capturing five things once — rate floor (PAYG & ABN), locations & onsite tolerance, role types & seniority, hard-no's, and eligibility+obtainability — via lightweight inputs, import-assist, and progressive depth. Red rules are user-set here (§7a). | 2026-08-06 |
| D8 | **Ambiguous clearance** | When "must hold" vs "can obtain" can't be told apart, show **amber + "verify"** — never a silent red. Never bin a winnable role on a guess. | 2026-08-06 |
| D9 | **Reflections are private forever** | Raw reflections are the user's alone — never shown to agents/employers, never shared, never fed into cross-user signals. Candour depends on this being absolute. Scoring signals (e.g. agency track record) come from the *factual outcome log*, not private text. See §7b. | 2026-08-06 |
| D10 | **Interview is a first-class event** | Its timing enters the system via **calendar-invite ingestion** (primary) or manual entry (fallback); it drives the reflection prompt, which is offered immediately but is **skippable / snoozable / pausable**. See §7b. | 2026-08-06 |
| D11 | **Positioning: episodic + keep-warm** | Not an always-on daily companion. Primarily used during a search, riding the contractor cycle, with two low-effort keep-warm hooks: (1) a **contract-end trigger** that re-activates ~8 weeks before the current gig ends (end-date captured willingly), and (2) a passive **rate drip**. See §11. | 2026-08-06 |
| D12 | **Rate signal = observed advertised rates** | The keep-warm rate drip and any benchmarking come from **rates stated in ingested job ads** ("roles like yours advertise ~$X–$Y") — observed, not invented. When ads are blank/messy, say **"not enough recent data"** rather than force a number. | 2026-08-06 |
| D13 | **Tailoring is an in-app loop** | Tailoring happens **inside the product**, not external ChatGPT — otherwise the accept/reject signal that powers learned voice is lost. Human-in-the-loop, two-way; the AI never sends a statement unseen. See §7c. | 2026-08-06 |
| D14 | **Moat = atoms + voice; bootstrap with atoms** | The moat is **tagged evidence atoms** (built passively) + **learned voice** (captured implicitly from edits, never by rating drafts); outcome-weighting is a slow-burn bonus. Cold start is bridged by atoms, and in-app tailoring must be *obviously* faster than ChatGPT from the first use. See §7c. | 2026-08-06 |

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

```text
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

- **Eligibility facts** — location/SEQ, working rights/visa/citizenship, security clearance (Baseline/NV1/NV2), **plus obtainability** (am I a citizen / willing to be vetted, so I *could* get cleared?), professional registrations, notice period/availability, PAYG vs ABN setup. These are the first gate — but **not purely binary** (see the three-state rule below). A role requiring a clearance you can *obtain* is not a reject.
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
- **Reflections** — agent quality, interview notes, "didn't like this person," "what I'd do better." **The crown jewel** — recorded nowhere else on earth, un-scrapeable, and what makes the system genuinely *know* you. **Private forever** (D9); captured multi-modally and triggered off the interview event (see §7b).
- **Interview events** — time, who, where/how, promised next steps. Sourced from **calendar-invite ingestion** (primary) or manual entry, and the trigger for reflection capture (D10, §7b).
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

Onboarding captures, once, the Half-A facts that drive the day-one light — **all four categories below, in under 2 minutes:**

- **Rate floor** — on both bases (PAYG+super *and* ABN+GST).
- **Locations & onsite tolerance** — where I'll work, how many onsite days I'll accept.
- **Role types & seniority** — the titles/levels I actually want, so obvious mismatches drop out.
- **Hard no's / deal-breakers** — named clients, agencies, industries, or arrangements I refuse.
- **Eligibility & obtainability** — what I hold, and whether I can/will obtain clearances (the three-state rule).

**The 2-minute target is a constraint on *how*, not *whether*.** All five are captured, but via **lightweight inputs** (ranges, chips, toggles — not free-text forms), with **import-assist** (infer from an uploaded CV / pasted LinkedIn, confirm only the gaps) and **progressive depth** (ask the essentials now; drip-feed refinements over the first few roles when they're relevant). Depth without a chore.

### Eligibility is three states, not two (correction)

A clearance/registration requirement is **not** "hold it or you're out." The JD language matters, and there are three states:

1. **Hold it** — the role wants a *current* clearance you already have → fine.
2. **Can obtain it** — the role says "ability to obtain" / "eligible for" a clearance, and you're a citizen willing to be vetted (many roles sponsor this) → **not a red; this is green/amber, keep it in play.**
3. **Can't meet it** — the role needs a clearance held *day one* that you don't have, or requires citizenship/working rights you can't satisfy → **red.**

**Only state 3 is an instant reject.** Conflating states 2 and 3 wrongly bins winnable federal/sponsored roles. So the extraction has to read *how* the requirement is phrased ("current NV1" vs "ability to obtain NV1"), and onboarding captures the user's **obtainability** (eligible/willing to be vetted?) as a field — not just what they *hold*. This is a system field, captured once; the platform never needs to interrogate the person beyond it.

**Ambiguous requirement → amber, never a silent red.** When extraction can't tell "must hold" from "can obtain," the light shows **amber with a "clearance requirement unclear — verify"** flag. A winnable role is never silently binned on a guess.

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

- **Clearance: none currently held — but obtainability TBD (citizenship / willingness to be vetted).** → Roles requiring a clearance *held day one* are red; roles saying *"ability to obtain"* stay in play if the founder is eligible and willing. **Correction to the earlier over-narrowing:** the pool is **not** just state-gov + private — it includes federal/sponsored roles where clearance is obtainable. The true auto-red is only state 3 above. (Where the founder isn't eligible/willing to obtain, the state-gov + private SEQ pool is the fallback.)
- **Capture tolerance: almost nothing typed** — reinforces D6.

*(Personal facts like the founder's own rate floor, clearance obtainability, and locations are **captured by onboarding at use time** — they're system fields, not things this document needs to pin down. We design the fields, not the founder's answers.)*

## 7b. Reflection capture & the interview as a first-class event

Reflections are the crown-jewel data (§6, Half B) — the candid, subjective residue nothing else on earth records. This section defines how it gets captured without becoming a chore, and it surfaced a **new requirement**.

### The new requirement: the interview must be a known event

You can't prompt for a reflection unless you know an interview *happened*. So the **interview is a first-class lifecycle event**, and its timing has to come into the system:

- **Primary source: the calendar invite.** When an interview is booked, it usually arrives as a calendar invite — so **calendar ingestion is a capture source**, not a nice-to-have. It seeds the interview event (time, who, where/how) with near-zero typing, consistent with the extraction-first principle (D6).
- **Fallback: manual entry** of the interview date/time, for when no invite exists.

This also enriches the role record: who I'm meeting, when, and the promised next steps.

### The prompt: offer immediately, but always dismissible

When the interview's end time is known, **offer the reflection right away** — but never trap the user. The prompt must support **skip / snooze / pause / reschedule**. It's an invitation in a raw emotional moment, not a demand. (When timing *isn't* known, reflection is still available manually anytime.)

### Capture is multi-modal — the user picks in the moment

No single input wins; support **all of them** and let the user choose by mood and situation:

- **Voice note, auto-transcribed** — ramble for 30 seconds while wired or deflated; lowest friction.
- **Quick taps** — mood, would-I-take-it, red-flag y/n.
- **Free text** — when they want control.
- **A few prompted questions** — light guidance when they want it.

### What a reflection captures (two classes of data)

All four dimensions earn their place — but they split into two classes with very different rules:

| Dimension | Class |
|---|---|
| **How I performed** — what landed, what I fumbled, what I'd say better | Subjective / private |
| **Do I even want it?** — gut feel on taking the role | Subjective / private |
| **Red flags & people** — "didn't like this person," bad vibe, culture warnings | Subjective / private |
| **Process & logistics** — who I met, next steps, timelines, what they asked | Factual / context |

### The privacy line — ironclad, and it has a design consequence

**Raw reflections are private forever (D9).** Never shown to agents or employers, never shared, never surfaced anywhere the user didn't put them. **Candour is the whole value, and candour depends on this being absolute.**

This draws a hard boundary that reconciles with the scoring model:

- **Factual outcome/event data** (applied, ghosted, progressed, interviewed, rejected) *can* feed winnability scoring — and, later, opt-in anonymised aggregates. This is behaviour, not confession.
- **Raw private reflections** ("this agency's people were useless") **never** feed cross-user signals or leave the user.

So when §7/§8 talk about "agency track record," that signal is built from the **factual outcome log**, *not* from private candid text. Two data classes, two rulebooks.

## 7c. Stateful tailoring — where the moat actually lives

The tailoring loop is not "another CV optimiser" — it's the mechanism that builds and spends the moat (R3). Three things, in dependency order:

### The moat is atoms + voice, not stored CVs

- **What it is NOT:** storing your CV. That's trivially copyable — a competitor's user just pastes theirs into a cold model.
- **Moat #1 — tagged evidence atoms.** Hundreds of your accomplishments, decomposed and tagged by capability, **built passively** (from uploaded CVs, past suitability statements, and every tailoring session) — never hand-entered. A cold prompt only gets the 2-page CV you pasted; the app reaches for the *right buried achievement* for *this* JD.
- **Moat #2 — learned voice.** Which phrasings and framings you accept vs reject, learned across many statements, so drafts already sound like you instead of generic AI-slop you beat into shape.
- **Moat #3 — outcome-weighting** (which statements got interviews) is a **slow-burn bonus, not a launch claim** — the feedback signal is sparse, delayed, and confounded. Stake the moat on #1 + #2; let #3 accrue.

### Voice is captured implicitly — tailoring must be in-app

Moat #2 only exists if the system **watches you tailor**. In your current ChatGPT workflow every accept/reject signal is thrown away. So:

- **Tailoring happens in-app — non-negotiable.** External ChatGPT loses the signal and moat #2 never forms.
- **Captured implicitly, never by rating drafts.** The statement you finally send, and the edits you made to get there, *are* the signal — kept sentences are positives, rewritten ones negatives. Same passive-capture principle as everywhere else.
- **Human-in-the-loop, two-way** — the AI drafts and iterates *with* you; it never fires off a statement unseen.

### The cold-start bootstrap — atoms earn the switch, voice compounds it

The chicken-and-egg: it needs in-app use to learn your voice, but needs a learned voice to beat ChatGPT and earn the use. Bridged by **atoms, not voice**:

- Day one the app can't sound like you yet — but it starts from your **pre-loaded atoms + the JD already in-system**, so you skip re-pasting and example-hunting. That alone makes it faster than a cold prompt *on the first use*.
- That day-one speed earns the switch; voice then quietly compounds over the following weeks.
- **The bar:** in-app tailoring must be *obviously* faster than ChatGPT from the very first use, or the habit wins and the voice signal is never captured. This is a hard product requirement, not an aspiration.

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
4. ~~**Reflection capture UX**~~ — **Resolved (§7b, D9/D10):** multi-modal capture, offered off a known interview event (calendar-ingested), always skippable, private forever. Still open underneath: **calendar-ingestion mechanics** — which calendars, how invites are matched to the right role record, and how to detect an interview vs any other meeting.
5. **Motivation & dignity as design requirements** — the product does psychological work, not just functional. How does "this took 4 minutes and is building into something" replace "this took 3 hours and vanished"?
6. ~~**The spine's decision surface**~~ — **Resolved (§7a):** minimum record = ref + rate + title/client/source/closing (+ JD text captured); red rules are personal and set at onboarding; reasons have trust tiers. Still open underneath: how good extraction has to be to feel effortless (ties to Q3-underneath).
7. ~~**Rate floor & onboarding set**~~ — **Resolved (D7, §7a):** under 2 minutes; captures rate floor (PAYG & ABN), locations & onsite, role types & seniority, hard-no's, eligibility+obtainability; lightweight inputs + import-assist + progressive depth. Still open underneath: the exact input widgets that make five categories feel like two minutes.

## 10. Explicitly out of scope (for now)

- Any technology, architecture, or implementation decisions.
- A standalone "optimise my CV / LinkedIn" tool — that already exists and is commoditising; we build the *end-to-end thread*, not another point solution.
- Horizontal launch across all user types simultaneously — deferred until the contractor wedge is won.
- Employer/recruiter-side product — candidate-first; revisit only with eyes open on the conflict it introduces.

## 11. Risks & assumptions we're betting on

The load-bearing beliefs under the whole product. Each box we design assumes these hold. Being tested through the grilling sessions.

| # | The bet | Status | How we'll know it's true |
|---|---------|--------|--------------------------|
| R1 | **It survives between searches.** A low-frequency tool that only opens during a hunt lets the profile rot and the memory never compounds. | **Addressed (D11/D12).** Positioned episodic + keep-warm: contract-end trigger + observed-rate drip, riding the short contractor cycle rather than fighting frequency. | Users return via the re-activation trigger; the drip earns an open. Still a real risk if neither hook pulls. |
| R2 | **n = 1 generalises.** Built from the founder's scars — but is the burnout a *market* problem or just a *me* problem? | **Open — highest unaddressed risk.** | A handful of other SEQ contractors recognise the loop and the demoralisation without prompting. (A validation activity, not a design decision.) |
| R3 | **The statefulness moat is real.** "Accumulating memory makes cycle 400 cheaper and better than a cold prompt." | **Addressed in design (D13/D14, §7c).** Moat staked on atoms + voice; in-app tailoring captures the voice signal; atoms bootstrap the cold start. Validated only by building it. | In-app tailoring is *obviously* faster than a cold ChatGPT prompt from the first use, and drafts sound more like the user over time. |

---

## Core principles (the test every decision must pass)

1. Shrink **effort × uncertainty × no-feedback** — the named villain.
2. **The thread is the product** — continuity and memory, not any single box.
3. **The moat is accumulating memory**, not generation or search.
4. **Targeting and quality over volume and speed** — help make better decisions, not submit more applications.
5. **Be brave enough to say "don't apply."**
6. **The user should never re-enter what the system already knows** — capture passively; manual entry only for what can't be seen, and make even that frictionless.
7. **Win the Australian contractor wedge completely before generalising.**
8. **Raw reflections are private forever** — the candour is the value, and it only exists if the user knows it never leaves them.
9. **Never bin a winnable role on a guess** — ambiguity resolves to amber-and-verify, not a silent red.
10. **No fabricated numbers** — every figure shown (rates, benchmarks) is *observed* from real data; when there isn't enough, say so rather than invent one.
