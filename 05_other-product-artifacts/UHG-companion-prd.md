# Companion: AI Chatbot for Optum Member & Provider Support — PRD

## 1. Problem Statement

Optum, UHG's largest business unit, routes the majority of patient and provider questions — including simple, repetitive ones about benefits, coverage, claims, and billing — to live agents. This drives long wait times, poor user experience, and roughly **$57M/year in operational spend**. The volume is dominated by routine, low-complexity queries that don't require a human agent to resolve, meaning the current model spends premium (human) capacity on commodity work.

**Cost of inaction:** support costs and wait times continue to scale linearly with query volume, with no structural relief, while consumer expectations for instant, self-service support (set by other digital health and fintech experiences) continue to rise.

## 2. Goal & Success Metrics

Deploy Companion as the first point of contact for member/provider support, shifting routine volume to self-service and improving the experience for everything that still needs a human.

- **Resolution rate:** 50% of interactions resolved without escalation to a live agent
- **Experience:** measurable lift in CSAT vs. current agent-first baseline
- **Cost savings:** $5M in the post-MVP period, scaling to **$30M/year by 2026**
- **Doc status:** decision-ready — this PRD is meant to greenlight build and align execution, not to explore alternatives

## 3. Audience & Use of This Doc

This PRD serves three audiences:
- **Engineering** — scopes what to build for the SoCal MVP and the integration surface (claims, benefits, provider directory)
- **Leadership** — the business case and phased investment (MVP savings → scaled savings by 2026)
- **Support operations** — how escalations change: volume mix, warm-transfer handoff, and expected impact on average handle time (AHT)

## 4. Context & Constraints

- **Timeline:** MVP live in Southern California by **February 2025**
- **Integration dependencies:** claims systems, benefits systems, provider directory — Companion's core differentiation depends on deep UHG systems integration, not a generic chatbot layer
- **Compliance:** personalization uses member data and must be HIPAA-compliant by design, not retrofitted
- **Escalation path:** complex queries route in-app to live agents with context passed via warm transfer, intended to lower AHT rather than simply deflect volume

## 5. Recommendation / Proposed Solution

Build Companion as an AI-first triage and self-service layer in front of the existing live-agent support model — not a replacement for agents. Companion should:
- Give instant answers and handle self-service for routine benefits/coverage/claims/billing questions
- Use healthcare-specific intelligence and HIPAA-compliant member data to personalize responses, rather than generic FAQ matching
- Warm-transfer unresolved or complex queries to agents with full context attached, so agents start from where Companion left off instead of re-asking the member
- Improve over time via continuous learning from resolved and escalated interactions

This is the recommended approach because it directly targets the highest-cost, lowest-complexity share of ticket volume first, while preserving the human path for everything Companion can't or shouldn't resolve.

## 6. Scope

**In scope (MVP):**
- SoCal launch, live by Feb 2025
- Self-service for benefits, coverage, claims, and billing questions
- In-app routing to live agents for complex queries, with context passed via warm transfer
- Integration with claims, benefits, and provider directory systems

**Explicitly out of scope (MVP):**
- Full replacement of live agents — Companion is a first-contact layer, not an agent substitute; complex cases still route to humans
- Geographic expansion beyond SoCal
- Clinical judgment calls and claims disputes — these remain agent-handled, not automated

## 7. User Outcomes / Requirements

- **Members/patients** get instant answers to routine questions without waiting in queue, and a smooth handoff (no repeating themselves) when a human is needed
- **Providers** get the same self-service and escalation path for their support needs
- **Support agents** receive escalations with member context already attached, reducing AHT instead of just reducing their call volume
- **Compliance/security** requirements are met by design: personalization draws on member data under HIPAA-compliant handling from day one

## 8. Risks & Open Questions

- Resolution-rate target (50%) is aggressive for a first MVP — what's the fallback plan or revised target if early SoCal data comes in lower?
- Savings trajectory ($5M → $30M/year by 2026) implies a multi-region rollout — timeline and scope for expansion beyond SoCal are not yet defined in this PRD
- Continuous learning loop needs an owner and a feedback mechanism (from both resolved and escalated interactions) — not yet specified
- Dependency risk: MVP timeline (Feb 2025) is tight given the number of system integrations (claims, benefits, provider directory) — integration readiness should be confirmed with each owning team

## 9. Timeline / Milestones

- **Feb 2025:** MVP live in Southern California
- **Post-MVP:** $5M in savings realized
- **By 2026:** savings scale to $30M/year

Open question: no milestones are defined between MVP launch and the 2026 target — the scaling plan (additional regions, expanded query coverage) needs to be sequenced. See Risks & Open Questions.
