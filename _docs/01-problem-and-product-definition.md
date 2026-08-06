# Career Management Platform: Problem and Product Definition

> **Status:** A living document. This is our thinking written down, not a build spec.
> We have not made any technology or design decisions yet, on purpose.
> **Last updated:** 2026-08-06

A quick note on language: this document is written in plain English. A few real-world
terms from Australian contracting stay as they are, because they are the actual words
used in the market: *suitability statement*, *Authority to Represent (ATR)*, *Consent
Form*, *Dochub*, *PAYG* and *ABN* (two ways a contractor can be paid and taxed),
*super*, *day rate*, *security clearance* (Baseline / NV1 / NV2), *SEEK*, *LinkedIn*,
*SmartJobs*, and a job's *reference number*.

---

## Decisions log

The decisions we have made and agreed. Settled unless we revisit them here.

| # | Decision | What we chose |
|---|----------|---------------|
| D1 | How the app tells you whether to apply | A simple **red / amber / green** signal plus **one short reason** (for example, "needs a clearance you don't have"). Quick to read, easy to trust. |
| D2 | How jobs get into the app | **A mix.** The reliable base is you pasting a link or forwarding an email. On top of that, a browser helper and automatic pulling-in of jobs where it works. The app must still be useful even if only the manual base works. |
| D3 | What we build first | The **tracker**: the app's running memory of every job, action, agency and outcome. It is useful even if you type things in by hand, and everything else builds on it. |
| D4 | How it makes money | **Left open on purpose.** Decide later once we've proven people want it. Design so we can still choose to charge job seekers *or* charge employers/recruiters later. |
| D5 | The "don't bother" rules | Four rules that mark a job red, all switched on: (1) pay below your minimum, (2) you can't meet the requirements, (3) wrong location or too many office days, (4) you've already seen it. Note: requirements like clearance have three states, see §7a. |
| D6 | How details get captured | **The app reads them for you.** You paste a link or forward an email and the app pulls out the title, client, pay, reference number and closing date. You only fix mistakes. Reading this accurately is a core requirement, not a nice extra. |
| D7 | Setup (first-time questions) | **Under 2 minutes.** Ask five things once: your minimum pay (both PAYG and ABN), where you'll work and how many office days, the roles you want, your absolute no's, and what you're eligible for. Use quick taps and sliders, fill in what it can from your CV, and ask the rest gradually. |
| D8 | When a clearance requirement is unclear | If the app can't tell whether you must already hold a clearance or just be able to get one, show **amber and "please check"**. Never quietly reject a job on a guess. |
| D9 | Your private notes stay private, forever | Your honest notes ("didn't like this person") are yours alone. Never shown to agencies or employers, never shared, never used in anything that touches other users. The app's judgements about agencies come from **what actually happened** (did they reply, did you get an interview), not from your private notes. See §7b. |
| D10 | Interviews are a proper event in the app | The app learns when an interview is happening from a **calendar invite** (or you enter it). That's what prompts you to jot a reflection afterwards. The prompt can always be skipped, delayed or paused. See §7b. |
| D11 | What the app is: a job-hunt tool with small reasons to return | **Not** a daily app you're expected to live in. Mostly used while job hunting. Two small things bring you back between hunts: (1) it knows when your current contract ends and wakes up about 8 weeks before, and (2) it quietly shows what similar jobs are paying. See §11. |
| D12 | Where pay figures come from | Only from **real numbers stated in job ads** the app has already seen ("jobs like yours are advertising about $X to $Y"). Never invented. If there isn't enough real data, it says so. |
| D13 | Writing happens inside the app | You do your CV and suitability-statement writing **in the app**, not in ChatGPT. That's the only way the app can learn how you like to write. You and the app work on it together, and nothing is ever sent without you seeing it. See §7c. |
| D14 | Why ChatGPT can't just replace this | Two things the app builds up that a fresh ChatGPT chat never has: a growing library of **your achievements** (collected automatically, never typed in by hand) and a feel for **how you write** (learned quietly from your edits). On day one the achievements alone make it faster than starting cold. See §7c. |
| D15 | Three ways to build an application pack | You can **forward the agency's email** (the app matches it to the job and works out what's needed), have a pack **prepared in advance** when you apply, or build one **on demand**. If the app isn't sure which job an email belongs to, it asks rather than guessing. See §7d. |
| D16 | Government forms: just track them for now | The app does **not** fill in or sign the Consent Form or Authority to Represent (those live in Dochub). You handle those. It **does** record which agency is representing you for which job, so you don't get submitted twice by mistake. See §7d. |
| D17 | How we check other people want this | **Build for yourself first, no upfront interviews.** The founder is confident from lived experience, so the first proof is real results on the founder's own applications. The network of contractors already known is kept as a safety net to sanity-check anytime (no cold outreach). See R2 in §11. |
| D18 | What we build first (the first slice) | **"Find jobs and tell me if they're worth applying for."** One thin slice end to end: quick setup, capture a job (paste or forward, not auto-search yet), and show the red/amber/green signal with a reason. The writing help is the **second** slice. See §12. |
| D19 | How the app protects motivation | **Make the growing asset visible**, as one connected chain, not separate tricks: your profile and reusable pieces visibly grow, that produces better outcomes (replies, interviews), and that saves you time. Show the whole chain (grew, so this happened, so you saved this), because effort vanishing into silence is what caused the burnout. |

---

## 0. How to read this document

This is the shared brain for the product. It sets out **what problem we're solving, who
for, and why.** It comes from real, lived experience as an Australian government IT
contractor, not from a market report.

It stops short of features, screens and technology on purpose. When we do start designing
those, they have to trace back to something on this page. If a feature idea doesn't serve
a problem written here, it doesn't belong.

Everything here is provisional and meant to be argued with. Things we still haven't
settled are listed in §9.

---

## 1. The problem, in one paragraph

Managing a career in Australia is scattered, repetitive and demoralising. You enter the
same information again and again across SEEK, LinkedIn, recruiters and government portals.
Every job wants a fresh, tailored CV and suitability statement, written from scratch, at
the exact moment you know the least about whether it's even worth writing. Then you send
it off and usually hear nothing back. Throughout, you (the candidate) are the person with
the least information and the least power in the room, and the whole process slowly trains
people to give up.

## 2. The real problem (not the obvious one)

The obvious version is "too much re-typing across too many sites." That's real, but it's
only the surface. If we build against just that, we end up with a slightly nicer CV
builder in a crowded market.

Two deeper problems sit underneath:

1. **You're always the least-informed person in the room.** You don't know what a job
   really pays, whether it's genuinely open, whether the recruiter is working for you or
   the client, whether an offer is good, or what your smartest next move is. The re-typing
   is annoying, but **making big decisions blind is what costs people years and thousands
   of dollars.**
2. **Huge decisions, made rarely, with no coach.** People make maybe 8 to 12 big career
   moves in a whole lifetime, each one stressful, each one without a trusted advisor who
   knows both you and the market. Wealthy people have mentors and career coaches. Everyone
   else has a mate's opinion and a Google search.

### What actually causes the burnout

The pain isn't just "time." It's three things stacked on top of each other:

- how much **effort** each application takes,
- how **uncertain** the outcome is, and
- how little **feedback** you ever get.

You put your biggest effort (a tailored suitability statement) in at the point of least
information, and get nothing back to tell you if it mattered. Do that hundreds of times
into silence and you burn out. That's the machine we're trying to break. **Every decision
we make should reduce at least one of those three things.**

## 3. Who this is for

**Australian contractors, starting with Queensland government and private IT contractors
around Brisbane.**

We're deliberately starting narrow, with one group we understand deeply, rather than
trying to serve everyone at once:

- **The pain comes back again and again.** A new contract every 6 to 12 months, forever.
- **There's real money in it.** Day rates are high enough that saving time and negotiating
  a better rate easily pays for the product.
- **The value is easy to see.** "You're a bit under the going rate," or "don't waste your
  time on this one."
- **They naturally come back.** Extensions and new contracts keep people returning, which
  is exactly the problem that kills most career apps (people use them once and forget them).
- **They're badly served today.** Overseas tools get none of the Australian and government
  details right.

Serving everyone (permanent staff, graduates, executives, career changers) is the
**long-term goal**, but a dangerous place to *start*. Win this one group completely first.

### Australian details that genuinely change the product

- **Comparing total pay is hard here.** "Package including super" versus "plus super"
  (super is 12% from July 2025), salary packaging, health and charity caps, novated leases.
  Two offers with the same headline number can be worth very different amounts.
- **The contractor world.** Day rates, agency margins, and two ways of being paid: PAYG
  (for example $100/hr plus super) or through an ABN ($112/hr plus GST). Plus extensions
  and the tax rules around all of it.
- **Government hiring is its own world.** Set pay levels, merit-based selection, addressing
  selection criteria, and **security clearances** (Baseline / NV1 / NV2) as a hard filter
  on who can even apply.
- **Authority to Represent.** Only one agency can put you forward for a given job. If two
  submit you for the same job, you can be knocked out. So who represents you for which job
  actually matters.
- **Working rights and visa status** are a first filter in a lot of hiring.
- **Registrations and clearances** are hard, checkable facts about who's eligible.
- **"Tall poppy" culture.** Australians are uncomfortable blowing their own trumpet, which
  makes CVs, LinkedIn and interviews genuinely harder here. Helping people sell themselves
  in a way that still sounds Australian (not American hype) is a real opportunity.

## 4. The lived process this is built from

The exact loop the product exists to break, as actually experienced:

1. **Endless scrolling** on SEEK, LinkedIn and SmartJobs. Hours of it. Clunky sites. The
   same job showing up under three different agencies.
2. **One-click "apply,"** which is mostly for show. It just drops your details into an
   agent's inbox. A computer may or may not read it, a person may or may not look. You get
   no feedback either way.
3. **The agent gets interested (or doesn't).** If they do, you get an email (like the
   RoadTek one, reference `1651209`): now send an updated CV in Word, now write a one to
   two page suitability statement for this job, now sign the Consent Form and Authority to
   Represent in Dochub.
4. **Hours of work** putting together a tailored pack for this one job.
5. **Silence.** Unless you're one of the few picked for interview.
6. **Repeat, thousands of times, until the energy is gone.**

Two things from experience that shaped everything below:

- **On writing:** "I upload my CV, the job description and the criteria, ask AI to write
  it, then go back and forth a hundred times." The core problem is that the AI has **no
  memory**. It doesn't know you or your last 400 statements, so you re-teach it how you
  write every single time.
- **On fake jobs:** "I've honestly never known whether a job is real. Is there a way to
  tell?" If someone who has applied thousands of times can't tell, then no single person
  can. Nobody has the information. That's not naivety, that's the gap in the market.

## 5. The core idea: joining the steps up is the product

Every single step already exists as its own product: job search, CV writer, application
tracker, interview-prep tool. **None of them talk to each other, or remember you.** The
thing that doesn't exist is the joined-up thread running through all of them.

This is clearly **not** "another CV or LinkedIn tidier." It's the **whole process, end to
end,** held together by one memory of you.

### The loop that builds on itself

```text
Search -> Score -> Write -> Track -> Interview -> Outcome
   ^                                                 |
   |__________  feeds back in  ______________________|
        (the scoring and your profile get smarter)
```

Every action leaves something behind that makes the next round quicker and smarter:

- The jobs you track teach the app which agencies and job types actually go somewhere
  **for you.**
- Each statement you write (with your input) adds to your profile, so the next one starts
  closer to how you write. The back-and-forth shrinks over time.
- Each outcome you record (interview, silence, "this agent is useless") is exactly the
  feedback the market never gives you, and it sharpens "should I apply?" for next time.

**The hard-to-copy part is the memory that builds up, not the writing.** AI writing is
becoming cheap and everywhere. Search is the thing the big sites guard hardest. What's
defensible is the memory that makes your 400th application a fraction of the effort of
your first, and a better one.

### A deliberate choice about what kind of product this is

Making applications cheaper must **not** quietly turn into "apply to more." The cure for
burnout is **less effort per application, plus real feedback, aimed at fewer, better-chosen
jobs.** A product brave enough to say "don't apply to any of these today" is the one that
gives you your energy back. Quality and aim over speed and volume.

## 6. The career memory (the core the rest plugs into)

This is the heart of the app. "Should I apply?" isn't a feature we build in isolation. It's
worked out from three things: what the app knows about **you**, what it knows about **this
job**, and what it has learned from **every job before this one.**

**The rule we hold ourselves to:** a piece of information earns its place only if it helps
with one of four things: does the job match you, is it worth applying for, writing your
application, or your private notes. If it helps with none of those, we don't store it.

The memory has two clearly separate halves, plus a scoring layer worked out from them.

### Half A: you (changes slowly, outlives any one job)

Your single source of truth. Jobs come and go; this builds up.

- **Eligibility facts:** where you are, your working rights and citizenship, security
  clearances (Baseline / NV1 / NV2), and whether you could *get* a clearance if you don't
  already have one (are you a citizen, willing to go through vetting). Also registrations,
  notice period, and whether you work PAYG or ABN. These are the first gate, but not a
  simple yes/no (see the three-state rule below). A job that needs a clearance you could
  get is not an automatic no.
- **Your preferences:** permanent versus contract, minimum pay, locations, industries,
  roles you want, and absolute no's. This is what "does it match me" is measured against.
- **Your achievements, in small reusable pieces.** This is the most important design idea
  in the whole memory. Not one big CV blob, but lots of individual, tagged accomplishments
  ("led the in-vehicle tracking rollout across X vehicles, delivered Y"). Writing a
  suitability statement then becomes picking the right pieces and shaping them to the job.
  **You never type these in by hand, because nobody thinks that way.** The app collects
  them for you from CVs you upload, jobs you write for, and the edits you make. This is what
  makes your 400th application cheap.
- **Your skills,** tidied into a common list so jobs can be matched against them, ideally
  lined up with how government describes the same skills.

### Half B: each job and its story (one per opportunity, always turning over)

The core unit of the tracker.

- **Keyed on the reference number.** `1651209` pulls the same RoadTek job, showing up via
  Hays and Peoplebank and SmartJobs, into **one** record. Without this the tracker is
  noise, and the risk of being submitted twice is invisible. For LinkedIn or private jobs
  with no reference number, match on title plus client plus pay plus the wording of the ad.
- **Job details:** reference, title, client, where it came from, the ad text, pay,
  duration, location, closing date, what's required.
- **Agency contacts (there can be several per job):** which agent, when, how, what they
  asked for, and **who holds Authority to Represent** for this job.
- **What you did:** where and when you applied, which versions of the pack you sent, forms
  signed.
- **Responses and outcomes:** replied, went quiet, shortlisted, interview, offer,
  rejection, each with a date.
- **Your private notes:** how good the agent was, interview notes, "didn't like this
  person," "what I'd do better." This is the most valuable thing here, because it's written
  down nowhere else and it's what makes the app actually know you. **Private forever** (D9).
  Captured in whatever way suits the moment, prompted by the interview (see §7b).
- **The interview itself:** time, who, where or how, what was promised next. Learned from a
  calendar invite or entered by hand, and it's what triggers your reflection (D10, §7b).
- **The score and the reason for it at the time,** so we can later check whether the app
  got it right and learn from it.

### The rule that ties the two halves together: keep a timeline, don't overwrite

Don't just record "status: rejected." Keep the **whole timeline**: applied Tuesday, agent
emailed Thursday, sent the pack Friday, silence, rejected three weeks later. Two reasons:

1. It gives you back the context when an agent pops up weeks later (the "wait, which job
   was this again?" problem).
2. The pattern and timing is exactly what teaches the app what a fake job's life looks like.

### Two ways things get captured, everywhere

- **Automatically,** from what you do in the app (made a pack, clicked apply).
- **Added by you,** for the things the app can't see: an agent's phone call, interview
  feedback, your private notes. This added-by-you information is the most valuable, so it
  has to be effortless to add (for example, a quick voice note after an interview).

## 7. Working out "should I apply?"

None of this is stored. It's worked out fresh each time from you, this job, and your history.

**Does it match you** (quick, works from day one, needs only your own information): can you
meet the requirements, do your skills overlap, is the seniority right, is the pay okay, is
the location okay. Rules you can't meet fail fast.

**Is it worth applying for** (the valuable part, gets better as your history builds):

- **Have I seen this already?** (matched on reference number)
- **Does it smell like a fake job?**
  - Things you could spot yourself, if you tracked them: the same job reappearing every few
    weeks, closing dates that keep getting pushed back, the same job blasted out by five
    agencies at once, or an agency that always asks for your pack and then goes quiet
    (building a database, not filling a real role).
  - Things only visible once there's enough history: an agency, client or role type where
    almost nobody ever gets an interview, which you'd never spot from a single ad.
- **This agency's track record with you:** do they ever actually move you forward?
- **Pay** versus your minimum and versus the market.
- **How long it's been sitting there.**

**Is it worth the effort:** given how winnable it looks, and whether you can reuse existing
material or have to write from scratch, is it worth your energy? This is where the app is
brave enough to say "don't bother with any of these today."

## 7a. The smallest job record, and the day-one signal

Because we're building the tracker first (D3), with the app reading details for you (D6),
and a red/amber/green signal (D1), the question is: **what's the least we need to record
about a job to still give a useful signal on day one?**

### The "don't bother" rules are yours, set during setup

The four red rules (D5) are **not fixed by us.** They're your own settings, chosen during
setup and changeable anytime. Your signal is tuned to your minimum pay, your eligibility,
your locations. This is how one simple signal can suit everyone: it's set by each person.

Setup captures, once, the facts that drive the day-one signal. All five below, in under
two minutes:

- **Minimum pay,** both ways (PAYG plus super, and ABN plus GST).
- **Locations and office days** you'll accept.
- **Roles and seniority** you actually want, so obvious mismatches drop out.
- **Absolute no's:** named clients, agencies, industries or arrangements you refuse.
- **Eligibility:** what you hold, and what you could get (the three-state rule).

**The two-minute target is about *how* we ask, not *whether*.** We still capture all five,
but with quick taps and sliders (not long forms), by filling in what we can from an uploaded
CV or LinkedIn and only asking about the gaps, and by asking the deeper stuff gradually over
your first few jobs. Depth without the chore.

### Eligibility has three states, not two

A clearance or registration requirement is not simply "have it or you're out." The wording
matters, and there are three cases:

1. **You hold it:** the job wants a current clearance you already have. Fine.
2. **You could get it:** the job says "ability to obtain" or "eligible for," and you're a
   citizen willing to go through vetting (many jobs sponsor this). **Not a no. Keep it in
   play.**
3. **You can't meet it:** the job needs a clearance held from day one that you don't have,
   or citizenship or working rights you can't satisfy. That's a no.

**Only the third case is an automatic no.** Treating "could get it" as "can't have it"
wrongly throws away winnable jobs. So the app has to read *how* the requirement is worded
("current NV1" versus "ability to obtain NV1"), and setup records what you could get, not
just what you hold. It's a setting captured once. The app never has to interrogate you
beyond that.

**When the wording is unclear, show amber, never a silent no.** If the app can't tell "must
already hold" from "could get," it shows amber with "please check." A winnable job is never
quietly binned on a guess.

### Not all reasons are trusted the same

An important point: a rule being a deal-breaker for you is **not** the same as you trusting
the app's judgement on it. All four are deal-breakers, but you'd only skip a job *without
double-checking* when the reason is plain and checkable.

- **Trust it outright** (can confidently mark red, or even hide): pay below your minimum,
  and jobs you've already seen. Objective and checkable.
- **Show it, but let you decide** (never hidden): "you might not be eligible" (you trust
  your own read on that) and "this agency has a poor track record with you" (a judgement,
  and shaky until there's enough history).

**What this means:** the plain, checkable reasons can drive a confident red and are the
safest to build first. The judgement calls show up as amber with "here's why, you decide,"
and earn trust over time rather than assuming it. This lines up with the day-one problem in
§8.

### The smallest record for a day-one signal

Enough to check the trusted rules and rebuild context later:

- **Reference number** (or the fallback: title plus client plus pay plus ad wording). Powers
  "have I seen this?"
- **Pay** (and whether it's PAYG or ABN). Powers "below my minimum?"
- **Title, client, source, closing date.** Context, and the "which job was this?" fix.
- **The ad text** (captured, not typed). Used later for matching and writing, but not needed
  for the day-one signal.

Everything past this is a bonus. The signal works from the reference number, the pay and
your setup, all of which the app can capture with almost no typing.

### First user's details, and a correction on who we serve

Facts from the first real user (the founder):

- **No clearance held right now,** but whether they could get one is a setting (citizenship,
  willingness to be vetted). Jobs needing a clearance from day one are a no; jobs saying
  "ability to obtain" stay in play if they're eligible and willing. **Correcting an earlier
  over-narrowing:** the pool is not just state government and private work. It includes
  federal and sponsored jobs where the clearance can be obtained. The only automatic no is
  the third case above. (Where the founder isn't eligible or willing, state government and
  private Brisbane work is the fallback.)
- **Wants to type as little as possible,** which reinforces D6.

(Personal facts like the founder's own minimum pay and locations are captured by setup when
they use it. They're settings, not things this document needs to pin down. We design the
questions, not the answers.)

## 7b. Capturing reflections, and treating the interview as a real event

Your private notes are the most valuable thing the app holds, because they're written down
nowhere else. This section is about capturing them without it becoming a chore, and it
turned up a new requirement.

### The new requirement: the app has to know an interview happened

You can't be prompted to reflect unless the app knows an interview took place. So the
interview is a proper event in the app, and its timing has to get in somehow:

- **Main way: the calendar invite.** When an interview is booked it usually turns up as a
  calendar invite, so reading calendar invites is a real way things get captured, not a
  nice-to-have. It fills in the interview (time, who, where or how) with almost no typing.
- **Backup: you enter it** by hand when there's no invite.

This also fills in the job record: who you're meeting, when, and what was promised next.

### The prompt: offer it straight away, but always let you skip

Once the app knows the interview has finished, it **offers** you the chance to jot a
reflection right away, but never traps you. The prompt can always be skipped, delayed or
paused. It's an invitation in a raw moment, not a demand. (When the app doesn't know the
timing, you can still add a reflection anytime.)

### Capture it whatever way suits the moment

No single way wins, so support all of them and let you pick by mood:

- **A voice note** the app writes up for you. Ramble for 30 seconds while it's fresh. Least
  effort.
- **A couple of quick taps:** mood, would-I-take-it, any red flags.
- **Typing it out,** when you want control.
- **A few short questions** to guide you, when you want that.

### What a reflection captures (two very different kinds)

All four are worth capturing, but they split into two kinds with different rules:

| What you capture | Kind |
|---|---|
| **How I did:** what landed, what I fumbled, what I'd say better | Private |
| **Do I even want it:** gut feel on taking the role | Private |
| **Red flags and people:** "didn't like this person," bad vibe, warning signs | Private |
| **Facts and next steps:** who I met, next steps, timelines, what they asked | Factual |

### The privacy line: absolute, and it shapes the design

**Your private notes are private forever (D9).** Never shown to agencies or employers, never
shared, never surfaced anywhere you didn't put them. The honesty is the whole value, and
honesty only happens if you know it never leaves you.

This draws a hard line that fits with the scoring:

- **What actually happened** (applied, went quiet, moved forward, interviewed, rejected) can
  feed the "is it worth applying?" scoring, and later, with your permission, anonymous
  patterns across users. This is behaviour, not private opinion.
- **Your private notes** ("this agency's people were useless") never feed anything shared
  and never leave you.

So when the app talks about an "agency's track record," that comes from **what happened**,
not from your private notes. Two kinds of information, two sets of rules.

## 7c. Writing your applications: why ChatGPT can't just do this

The writing part is not "another CV tidier." It's how the app builds up, and then spends,
the thing that makes it hard to copy. Three points, in order:

### What's hard to copy is your achievements plus your writing style, not a stored CV

- **What it is NOT:** just storing your CV. Anyone can paste their CV into ChatGPT, so that
  alone is no advantage.
- **First: your achievements, in small pieces.** Hundreds of your accomplishments, tagged by
  skill, collected automatically from CVs, past statements and your edits. Never typed in by
  hand. A cold ChatGPT chat only has the two-page CV you pasted. The app can reach for the
  *right buried achievement* for *this* job.
- **Second: your writing style.** Which wordings you keep and which you change, learned over
  many statements, so drafts already sound like you instead of generic AI text you have to
  fix.
- **Third: what actually wins** (which statements led to interviews) is a **slow-burn bonus,
  not a day-one promise.** That feedback is thin, slow and hard to read cleanly. So we rest
  the case on the first two, and let the third build up.

### Your writing style is learned quietly, so the writing must happen in the app

The app can only learn your style if it **watches you write.** In your current ChatGPT
habit, every keep-this / change-that signal is thrown away. So:

- **Writing happens in the app.** This is non-negotiable. In ChatGPT the signal is lost and
  the app never learns your style.
- **Learned quietly, never by asking you to rate drafts.** The version you finally send, and
  the edits you made getting there, are the signal. Kept sentences are a yes, rewritten ones
  a no. Same "capture it automatically" idea as everywhere else.
- **You and the app together.** The app drafts and edits *with* you. It never sends anything
  you haven't seen.

### The day-one problem, and how we get past it

The chicken-and-egg: the app needs you writing in it to learn your style, but it needs to
already sound like you to be worth switching from ChatGPT. We get past it with **your
achievements, not your style:**

- On day one the app can't sound like you yet. But it starts from your ready-collected
  achievements and the job details it already holds, so you skip re-pasting your CV and
  hunting for examples. That alone makes it faster than starting cold, on the very first go.
- That first-day speed earns the switch. Your style then builds up quietly over the following
  weeks.
- **The bar:** writing in the app has to be *clearly* faster than ChatGPT from the very first
  use, or the old habit wins and the app never learns your style. This is a hard requirement,
  not a hope.

## 7d. The moment the agent asks for your pack

This is where the most time is currently wasted, and so where the app helps most: the moment
an agent gets interested and asks for the pack (the RoadTek email), where you currently burn
hours and lost the will to keep going.

### Three ways to build a pack (D15)

- **Forward the agent's email (main way):** the app matches it to the job it already knows
  (by reference number, or by client plus title plus pay), works out what's being asked for
  (CV, suitability statement, forms) into a checklist, and puts it together. The writing part
  (§7c) drafts the suitability statement from your achievements and the job it already holds,
  and the CV comes out in the format asked for.
- **Prepared in advance:** optionally have a ready-to-go pack the moment you apply, so it's
  waiting if the agent bites.
- **On demand:** build one yourself from the tracker anytime.

**It asks rather than guessing:** a reference number matches confidently. When the fallback
match is uncertain, the app **asks you to confirm the job** rather than quietly attaching it
to the wrong one (in line with principle 9).

### Government forms: just tracked for now (D16)

The Consent Form and Authority to Represent live in Dochub. For now the app does **not** fill
them in or sign them. You do that. But it **does** record which agency is representing you for
which job, which is what stops you being submitted twice by mistake. Recording that fact is
not the same as owning the forms, and owning the forms is left for later.

## 8. Why the app starts useful and gets smarter (not clever on day one)

The app does not launch knowing everything:

- **"Does it match me" works from day one.** It only needs your own information.
- **The writing help and the tracker** (ending "which job was this again?") are useful
  straight away.
- **"Is it worth applying?" starts weak** with one user and no history. It **grows** as your
  own tracker fills up, then **grows further** as more people join and shared patterns emerge,
  something a brand-new competitor can't hand a new user on day one.

This is a strength, not a weakness. Early users who let the app build up their history get
something later rivals can't copy.

## 9. Still open (not yet settled)

1. **How the app tells you to apply:** settled as red/amber/green plus one reason (D1). Still
   open underneath: exactly which reasons we can produce on day one versus later.
2. **How it makes money:** left open (D4). Charging job seekers (honest, but they pay only
   while hunting) versus charging employers/recruiters later (more money, but pulls against
   "we work only for you"). Design so neither door is shut.
3. **Pulling in jobs automatically:** direction set (D2). Pasting and forwarding is the
   reliable base; a browser helper and automatic pulling-in come on top. Still open: how good
   the pasting/forwarding reading has to be to feel effortless.
4. **Capturing reflections:** settled (§7b, D9/D10). Captured however suits you, prompted off
   a known interview, always skippable, private forever. Still open underneath: the calendar
   details (which calendars, matching an invite to the right job, telling an interview apart
   from any other meeting).
5. ~~**Motivation and dignity as design goals**~~ **Resolved (D19).** Make the growing asset
   visible as one connected chain: your profile grows, that produces better outcomes, that
   saves you time. Show the whole chain, because effort vanishing into silence is what caused
   the burnout. Still open underneath: exactly how this shows up on screen (a job for the
   prototype).
6. **The smallest job record:** settled (§7a). Reference number, pay, title, client, source,
   closing date, plus the ad text captured. The red rules are yours, set at setup, and reasons
   are trusted differently. Still open underneath: how good the automatic reading has to be.
7. **Setup:** settled (D7, §7a). Under two minutes, five things, quick inputs, fill-in from
   your CV, ask the rest gradually. Still open underneath: the exact tap-and-slider design that
   makes five things feel like two minutes.

## 10. Deliberately not doing (for now)

- Any technology or design decisions yet.
- A standalone "tidy up my CV / LinkedIn" tool. That already exists and is becoming cheap. We
  build the joined-up process, not another single-purpose tool.
- Launching for everyone at once. That waits until we've won the contractor group.
- An employer or recruiter product. We're on the candidate's side first, and would only revisit
  this with eyes open about the conflict it creates.

## 11. The big bets we're making

The beliefs the whole product rests on. Everything we design assumes these hold. We're testing
them in the grilling sessions.

| # | The bet | Where it stands | How we'll know it's true |
|---|---------|-----------------|--------------------------|
| R1 | **People still use it between job hunts.** A tool only opened while hunting lets your profile go stale and never builds up. | **Addressed (D11/D12).** Positioned as a job-hunt tool with two small reasons to return (a contract-end wake-up and a quiet pay signal), riding the short contractor cycle. | People come back via the wake-up, and the pay signal earns an open. Still a real risk if neither pulls. |
| R2 | **This isn't just my problem.** Built from one person's experience. Is the burnout a whole-market problem or just a me problem? | **Carried, not tested (D17).** Founder is confident from years of living it and seeing others struggle, and chose to build for personal use first rather than run interviews. The network is there as a safety net to check anytime. | Founder's own real results using it, and, if doubt creeps in, a few honest chats with contractors already known (no cold outreach). |
| R3 | **The memory really does beat starting cold.** "The app gets cheaper and better than a fresh ChatGPT chat as it learns you." | **Addressed in the design (D13/D14, §7c).** Rests on your achievements plus your writing style; writing in the app captures the style; achievements carry the first day. Only proven by building it. | Writing in the app is clearly faster than a cold ChatGPT chat from the first use, and drafts sound more like you over time. |

## 12. Where we start building (the first slice)

We're building for the founder first (D17), and the win that keeps the founder motivated is
**finding jobs and knowing which are worth applying for**, not the writing. So the first slice
is exactly that, kept thin but running end to end (D18):

1. **Quick setup** (so there's something to score against): the five things from §7a, in under
   two minutes.
2. **Capture a job:** paste a link or forward an email, and the app reads out the details.
   This leans on the reliable base from D2. It is **not** auto-searching SEEK or LinkedIn yet;
   that comes later.
3. **Show the signal:** red / amber / green plus one short reason.

Two honest limits to hold in mind for this first slice:

- **The "search" here is capture, not magic.** You still bring the job to the app (paste or
  forward). Automatic pulling-in of jobs is a later addition, because it's the fragile part
  the big sites fight hardest.
- **Day-one scoring is the checkable half.** It can confidently handle pay, eligibility,
  location and "already seen." The cleverer half (is this a real job, is it worth it) needs
  history and grows over time, as set out in §8. Even the checkable half is worth it, because
  it clears the obvious no's straight away.

The writing help (§7c) is the **second** slice. This first slice still quietly builds the
memory underneath (your setup and the jobs you capture), so slice two has something to stand
on.

---

## The principles every decision has to pass

1. **Cut effort, uncertainty and silence.** These three are what cause the burnout.
2. **Joining the steps up is the product,** not any single step on its own.
3. **The hard-to-copy part is the memory that builds up,** not the writing or the search.
4. **Aim and quality over speed and volume.** Help people make better choices, not fire off
   more applications.
5. **Be brave enough to say "don't apply."**
6. **Never make people re-enter what the app already knows.** Capture it automatically. Only
   ask for what the app can't see, and make even that effortless.
7. **Win the Australian contractor group completely before going wider.**
8. **Private notes are private forever.** The honesty is the value, and it only exists if you
   know it never leaves you.
9. **Never reject a winnable job on a guess.** When unsure, show amber and "please check,"
   not a silent no.
10. **Never invent a number.** Every figure (pay, benchmarks) comes from real data. When
    there isn't enough, say so instead of making one up.
11. **Make effort visibly build.** Show the work accumulating into a growing asset that
    produces outcomes and saves time. Effort must never feel like it vanished into silence.
