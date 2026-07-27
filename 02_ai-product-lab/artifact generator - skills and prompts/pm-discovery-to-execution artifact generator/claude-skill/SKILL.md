---
name: pm-discovery-to-execution
description: Runs a full product discovery-to-execution pipeline for a product problem statement — sequencing it through Discovery, Persona Mapping, Empathy Map, Customer Journey Map, Business Model Canvas, North Star/Goals framework, Strategic Alternatives Evaluation, Prioritization, MVP Scope, PRD, Roadmap, GTM Plan, Feature Detail, User Stories, and a post-launch PMF check, using gated sub-prompts that pause for confirmation at each stage instead of drafting blind. Use whenever the user wants to take a raw product problem from discovery through to execution artifacts, asks to write a PRD, roadmap, GTM plan, business model canvas, prioritization framework, MVP scope decision, feature backlog, user stories, personas, an empathy map, a customer journey map, a North Star/KPI framework, or a strategic alternatives evaluation, asks to "run the pipeline"/"run the master flow," or continue/resume a prior stage, or is a PM building a product initiative end to end.
---

# PM Discovery-to-Execution Pipeline

A master orchestration skill that runs a product initiative through fifteen gated
stages, each powered by its own sub-prompt in `references/`. This file is the
sequence logic; it does not contain the actual stage instructions — those live in
the numbered reference files and are loaded one at a time, only when that stage is
active.

## How this works

1. **One stage at a time.** Identify which stage is active (see table below), then
   read *only* that stage's reference file with the `view` tool before responding.
   Don't pre-load the others — that defeats the point of keeping this lean.
2. **Each reference file has its own HARD GATE.** It will refuse to draft until its
   own Step 1 gaps are resolved. Respect that gate exactly as written in the file —
   do not skip it, soften it, or draft a "starter" version because the user seems in
   a hurry. The gate is the point: it's what keeps every downstream artifact
   evidence-based instead of invented.
3. **After Step 1, stop. Every time. No exceptions.** This is the rule most likely
   to get silently skipped, so it's stated plainly here in addition to each
   reference file's own wording: once you've either (a) asked the Step 1 gap
   questions, or (b) found no gaps and stated your read of each point in one line,
   your response ends there. Do not produce any part of Step 2 — no draft, no
   partial artifact, no "here's a preview while we wait" — in the same response,
   regardless of which of (a) or (b) applies. The user must send a reply (an
   answer, "proceed," or "use your best judgment") before Step 2 begins. If you
   notice yourself about to write Step 2 content in the same turn as Step 1, that
   is the signal to delete it and end the response instead.
4. **Carry state forward, don't re-ask.** Maintain a short running recap — the
   "Context So Far" block described below — and check it before asking any Step 1
   question. If a fact is already in the recap, state it back as a confirmed
   assumption instead of asking again. Re-derive only what each stage's own prompt
   explicitly says must be re-derived (e.g., Feature Detail always re-derives the
   feature breakdown even if audience/format carry over).
5. **One conversation, one stage in flight.** This skill runs stages sequentially
   within a single conversation. It does not run stages in parallel — a chat is
   single-threaded. If the user wants true parallel execution (e.g., Feature Detail
   and Roadmap running concurrently once PRD is locked), tell them this skill gives
   them the sequential version cleanly, and that parallel execution needs a
   Claude Code / Agent SDK build using subagents — don't attempt to fake parallelism
   by interleaving stages in one response.
6. **Open a new pipeline run with the flow diagram, before any Step 1 questions.**
   The very first response to a fresh problem statement (see "Starting or
   resuming" below) must render a visual overview of all fifteen stages, before
   Stage 1's gate questions begin. Keep this diagram plain: one box per stage
   showing its number and name, grouped under phase-name headers (Discovery /
   Direction / Strategy / Execution / Validate), connected by simple arrows in
   sequence, plus one loop-back arrow from Stage 15 to Stage 8. No legends, no
   annotation text, no scoring charts, no extra explanatory copy on the diagram
   itself — the stage and phase names are the whole point. Use whatever rendering
   capability is available in the environment (an inline diagram tool if present,
   otherwise an SVG/HTML file artifact) — the mechanism can vary, but the diagram
   itself cannot be skipped or deferred to "later," and it must stay in sync with
   the stage table below if stages are ever added, removed, or reordered.
7. **Honor each stage's own VISUALIZATION GATE.** Most reference files require a
   rendered visual (not prose) alongside their written output — see "Visual output
   by stage" below for the full list. Treat that requirement exactly as strictly
   as the HARD GATE: a stage with a VISUALIZATION GATE is not complete without its
   diagram in the same response, and the diagram must agree with the written
   content (same items, same scores/positions) — never a visual that contradicts
   or merely decorates the text next to it.

## The sequence

| # | Stage | Reference file | Needs as input | Produces |
|---|-------|----------------|-----------------|----------|
| 1 | Discovery | `references/01-discovery.md` | Raw problem statement | Hypotheses, open questions, risks/opportunities, named segments |
| 2 | Persona Mapping | `references/02-persona-mapping.md` | Stage 1 segments + evidence | Concrete personas per segment/sub-segment, each with a validation status |
| 3 | Empathy Map | `references/03-empathy-map.md` | Stage 2 personas only | Says/Thinks/Feels/Does + Pains/Gains + a Design Implication per persona |
| 4 | Customer Journey Map | `references/04-customer-journey-map.md` | Stage 2 personas + Stage 3 empathy maps | Stage-by-stage current-state journey, emotional arc |
| 5 | Business Model Canvas | `references/05-business-model-canvas.md` | Stage 1 output + Stage 2-4 persona/empathy/journey detail + problem statement | Segment-specific value props, cost/revenue logic |
| 6 | Goals & Measurement | `references/06-goals-measurement.md` | Stage 1 evidence + Stage 5 segments/value props + business objective | North Star metric + supporting pillar tree (or a trace-up to an existing one), instrumentation gaps |
| 7 | Strategic Alternatives Evaluation | `references/07-strategic-alternatives.md` | Stage 5 segments/value props + Stage 6 North Star + candidate strategic approaches | Scored comparison matrix, recommended direction |
| 8 | Prioritization | `references/08-prioritization.md` | Stage 1 hypotheses + Stage 4 journey opportunities + Stage 6 North Star + Stage 7 chosen direction + candidate themes/opportunities within it (theme-level by default — see that file's granularity check) | Ranked/scored opportunity list |
| 9 | MVP Scope Identifier | `references/09-mvp-scope-identifier.md` | Stage 8 ranked list + a hard constraint (date/geo/budget) + minimum viable outcome | Locked In/Out scope with defer triggers |
| 10 | PRD | `references/10-prd.md` | Stage 9 locked In-scope list | Problem, Recommendation, Scope, Requirements, Technical Considerations |
| 11 | Roadmap | `references/11-roadmap.md` | Stage 10 PRD scope (Now) + Stage 8 leftover items (Next/Someday) | Phased sequencing, Gantt + Now/Next/Someday |
| 12 | GTM Plan | `references/12-gtm.md` | Stage 10 PRD + Stage 11 roadmap phases | Positioning, channels, launch sequencing |
| 13 | Feature Detail | `references/13-feature-detail.md` | Stage 10 PRD only | Feature tickets w/ Given/When/Then ACs |
| 14 | Feature & User Story | `references/14-feature-story.md` | Stage 13 output only | Sprint-ready user stories |
| 15 | PMF Assessment | `references/15-pmf.md` | Real post-launch usage data (not available until after launch) | Signal-by-signal verdict → loops back to Stage 8 & Stage 11 |

**Phases (for the flow diagram and general orientation):**
- **Discovery** — Stages 1-4 (Discovery, Persona, Empathy Map, Journey Map). All
  user-understanding work sits inside Discovery, not as a separate phase — this
  matches standard Design-Thinking framing (empathy work is stage one, not a later
  add-on) rather than treating research as something bolted on after a first pass
  at the problem.
- **Direction** — Stages 5-7 (Business Model Canvas, Goals & Measurement,
  Strategic Alternatives). This is "what are we choosing to pursue and how will we
  know it's working," as distinct from Discovery's "what's true about the
  problem."
- **Strategy** — Stages 8-11 (Prioritization, MVP Scope, PRD, Roadmap).
- **Execution** — Stages 12-14 (GTM, Feature Detail, User Stories).
- **Validate** — Stage 15 (PMF), event-triggered, loops back.

**Dependency notes:**
- Stages 1→10 are a strict sequential spine. Each stage's gate depends on the
  prior stage's *confirmed* output, so don't jump ahead even if the user pastes a
  lot of context up front — still run each stage's own Step 1 against what's been
  confirmed so far.
- **Stage 2→3 is its own strict pipe within the spine**, same pattern as Feature
  Detail→Feature Story: Empathy Map (3) takes *only* Persona Mapping's (2) output
  as input and does not re-derive personas or segments itself.
- **Stage 4 needs both Stage 2 and Stage 3.** Customer Journey Map expands a
  persona and its empathy map across time; it does not run on a persona alone if
  an empathy map already exists in the conversation — richer emotional-arc detail
  depends on it.
- **Stage 4 has a second, optional invocation point later in the pipeline.** After
  Stage 10 (PRD) or Stage 13 (Feature Detail) is locked, Stage 4 can be re-run in
  **future-state mode** to validate that each proposed requirement/feature actually
  resolves a specific stage of the original current-state journey. This is a
  validation loop, not a new numbered stage — treat a request like "show the
  journey after the fix" as re-entering Stage 4 with the locked PRD/Feature Detail
  as additional input, never inventing improvements the PRD/Feature Detail doesn't
  actually contain.
- A persona's (Stage 2), empathy map's (Stage 3), or journey map's (Stage 4)
  validation status (evidence-grounded vs. hypothesis-based) must propagate
  forward — Business Model Canvas, Prioritization, and PRD should treat
  hypothesis-based implications as unvalidated input, not settled fact, until real
  evidence exists.
- **Stage 6 (Goals & Measurement) always checks first whether a higher-level North
  Star already exists** for this product line before building a new framework from
  scratch — see that file's Question 0. Don't skip this check even if the input
  seems to call for a fresh framework; a North Star built fresh for every
  individual initiative usually means one already exists one level up that this
  should trace to instead.
- **Stage 8 defaults to theme/opportunity-level candidates, not atomic features** —
  see that file's granularity check. If you construct Stage 8's candidate list
  yourself (nothing was given to score), building it at feature-level granularity
  means Stages 8→9→10→13 end up relabeling the same list four times instead of
  each doing distinct work — Feature Detail (13) specifically needs something left
  to decompose. Score themes at Stage 8; let features emerge at Stage 13, where
  they may split or merge differently than however the themes were first grouped.
- **Stage 8 (strategic prioritization) and backlog grooming are different
  activities — don't conflate them.** Stage 8 is a one-time Impact-vs-Effort pass
  over themes, done once per initiative. Ranking the Stage 14 story backlog is
  ongoing, sprint-by-sprint work, defaults to RICE (see Stage 14's Step 1 Q5), and
  isn't itself a numbered stage in this pipeline — it happens after Stage 14
  produces the backlog to rank.
- **Stage 7 evaluates the direction itself, Stage 8 ranks capabilities within it.**
  Don't let Prioritization (8) implicitly re-decide the strategic direction Stage 7
  already settled — if a Stage 8 candidate doesn't fit the Stage 7 chosen
  direction, flag the mismatch rather than silently including it. If the original
  problem statement already named a specific proposed solution, Stage 7 still
  evaluates it honestly against real alternatives — it does not treat the proposal
  as pre-validated just because it was stated first.
- **Stage 6's North Star and pillars should visibly inform Stage 7's evaluation
  criteria, Stage 8 Prioritization, and Stage 10 PRD's Goal & Success Metrics** —
  if a later stage's ranking or goal doesn't trace back to something in the
  Stage 6 framework (or its trace-up to an existing one), flag the gap rather than
  silently introducing a new, disconnected metric.
- Stage 13→14 is a strict two-step pipe, independent of Stages 11-12. It only
  needs the PRD.
- Stage 11→12 is its own pipe, independent of Stage 13-14. Roadmap needs the PRD
  and Stage 8's deferred items; GTM needs Roadmap's phase structure.
- Stage 15 doesn't run until real usage data exists — don't simulate or invent
  this data to run the stage early. If the user asks to "run the whole pipeline
  now," stop after Stage 14 and explain that Stage 15 waits for the MVP to
  actually ship and collect data.
- Stage 15's output is a loop, not an endpoint: its verdict feeds back into Stage 8
  (re-prioritize with new evidence) and Stage 11 (re-sequence the roadmap). Treat
  a request to "run the next phase" post-PMF as re-entering Stage 8 with the PMF
  findings added to Context So Far. If real usage data reveals a persona's
  hypothesis-based assumptions were wrong, also flag that Stage 2/3/4 may need a
  revision pass — the loop can reach back further than Stage 8 when the evidence
  gap was in the persona or journey, not just the priority order. This is also the
  natural trigger point for the Stage 4 future-state re-run described above, using
  real usage data instead of the PRD alone.

## Context So Far (maintain this across the conversation)

Keep a running, short block of confirmed facts — update it after each stage
completes, and reference it (don't restate its full contents to the user every
turn, just use it internally to resolve gates). Include at minimum:

- **Constraint(s):** e.g. launch date, geography, budget
- **Segments:** every distinct user/customer group named so far
- **Personas & validation status:** each persona from Stage 2, and whether it (and
  its Stage 3 empathy map, Stage 4 journey map) is evidence-grounded or
  hypothesis-based — carry this forward as-is, don't let later stages upgrade its
  confidence
- **Design Implications & journey opportunities:** the one-line "so what" from
  each Stage 3 empathy map, and the stage-level opportunities from Stage 4's
  journey map — these should visibly show up as rationale in Stage 8
  Prioritization and Stage 10 PRD's User Outcomes, not get lost after Stage 4
- **North Star & pillars (Stage 6):** the chosen North Star metric and its
  supporting pillar tree — or the existing higher-level framework it traces up to
  — so later stages reference it instead of inventing a parallel metric
- **Chosen strategic direction (Stage 7):** the alternative selected, and why —
  Stage 8 candidates should fit within this direction, not silently re-litigate it
- **Success metrics:** eventual target vs. MVP-floor, kept distinct (Stage 9
  exists specifically because these are often conflated in a first problem
  statement — if the user's original input states only one number, flag this
  ambiguity the first time it matters, rather than assuming which one is intended)
- **Locked decisions:** the In-scope list from Stage 9, the Recommendation from
  Stage 10, the phase structure from Stage 11 — i.e., anything a later stage must
  not contradict without flagging the conflict explicitly
- **Technical Considerations (Stage 10):** any NFRs, integration approach, or
  rollout/rollback details given or flagged `[RECOMMENDATION — needs
  confirmation]` — Stage 13's `TBD — Review Required` latency/throughput tags
  should trace back to what this section left open, not invent separate unknowns
- **Open questions carried forward:** anything a stage flagged as unresolved that a
  later stage might need

## Visual output by stage

Every stage below requires a rendered visual, not a text description of one, in
the same response as its written artifact:

| # | Stage | Required visual |
|---|-------|------------------|
| 1 | Discovery | — (no forced visual; prose hypotheses/risks/next-steps) |
| 2 | Persona Mapping | Persona Card (one per persona) |
| 3 | Empathy Map | Four-Quadrant Empathy Map (one per persona) |
| 4 | Customer Journey Map | Stage-by-Stage Journey Map |
| 5 | Business Model Canvas | 9-block Osterwalder grid |
| 6 | Goals & Measurement | North Star Metric Tree (or trace-up diagram if inheriting an existing one) |
| 7 | Strategic Alternatives Evaluation | Comparison Matrix (rendered table) |
| 8 | Prioritization | Prioritization Matrix (Impact vs. Effort 2x2) |
| 9 | MVP Scope Identifier | Scope Boundary Diagram (In/Out, rank visible) |
| 10 | PRD | — (text artifact for engineering; no forced visual) |
| 11 | Roadmap | Gantt timeline + Now/Next/Someday grid |
| 12 | GTM Plan | Positioning & Channel matrix + Launch Sequencing timeline |
| 13 | Feature Detail | — (ticket format; no forced visual) |
| 14 | Feature & User Story | — (backlog format; no forced visual) |
| 15 | PMF Assessment | PMF Signal Scorecard + Retention chart or Path-to-PMF timeline |

Stages 1, 10, 13, and 14 intentionally have no forced visual. Discovery (1) is a
narrative/hypothesis-forming exercise where a chart adds process overhead without
adding clarity at that early a point; PRD (10), Feature Detail (13), and Feature &
User Story (14) are artifacts written for engineering to build from (a PRD,
tickets, stories), and a diagram bolted onto them would pad the document rather
than help the reader, contradicting those files' own "no additions" DRAFT GATE. If
the user explicitly asks for a visual on any of these anyway (e.g., "show me the
feature dependencies as a diagram"), that's a reasonable one-off request —
accommodate it, but it doesn't change the stage's default requirement.

## Starting or resuming

- **New problem statement, no prior stage run:** render the full pipeline flow
  diagram first (see rule 6 in "How this works" above), then start Stage 1. Don't
  skip to a later stage just because the user's input looks detailed — Stage 1's
  own gate decides whether it's actually sufficient.
- **User says "skip discovery, I already know the problem" or similar:** you may
  waive a stage's Step 1 questions only if the user explicitly says so for that
  stage (matches each reference file's own "proceed / use your best judgment"
  escape hatch) — but still tell them what Context So Far you're assuming in its
  place, in one line, so the gap is visible rather than silently skipped.
- **User provides output from a stage run elsewhere (e.g., pastes a PRD they wrote
  outside this skill):** treat it as that stage's completed output, extract Context
  So Far from it, and move to the next stage — don't re-run a stage whose output is
  already in hand.
- **User asks to resume mid-pipeline:** ask which stage they're at if it's not
  obvious from the conversation, rather than assuming Stage 1.

## What this skill does not do

- It does not invent facts, dates, or metrics any more than each individual
  reference file already permits — the DRAFT GATE rules inside each file (no
  invented specifics, `[ASSUMPTION: ...]` tagging) still apply in full.
- It does not merge two stages into one response to save time. Each stage produces
  its own artifact; present them one at a time so the user can actually review and
  confirm before the next stage builds on it.
- It does not run Stage 15 (PMF) without real data, and does not fabricate a
  plausible PMF verdict to keep the pipeline moving.
- It does not build a fresh North Star framework at Stage 6 without first checking
  whether a higher-level one already exists to trace up to instead.
