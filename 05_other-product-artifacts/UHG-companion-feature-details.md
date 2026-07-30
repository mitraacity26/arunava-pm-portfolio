# Companion — Feature Detail Tickets
*Derived from: UHG-companion-prd.md | Audience: Dev team (estimating for build) | AC format: Given/When/Then*

---

## Feature 1: Self-Service Resolution

**Feature ID:** TBD
**Status:** TBD

**Problem:**
Optum routes the majority of routine, low-complexity member/provider questions (benefits, coverage, claims, billing) to live agents, driving long wait times, poor experience, and ~$57M/year in operational spend.

**Background:**
Query volume is dominated by routine questions that don't require a human agent to resolve — the current model spends live-agent capacity on commodity work.

**Timing:** Launch target: Feb 2025 (Southern California) to meet MVP live deadline.

**Product requirements:**
- Provide instant self-service answers for benefits, coverage, claims, and billing questions.
- Available to both members/patients and providers.

**Acceptance Criteria:**
- Given a member submits a routine benefits/coverage/claims/billing question, When Companion processes it, Then it returns an answer without agent involvement.
- Given a provider submits a routine support question, When Companion processes it, Then it returns a self-service answer without agent involvement.

**Value:** Directly targets the highest-cost, lowest-complexity share of ticket volume first, while preserving the human path for what Companion can't resolve.

**Metrics:**
- 50% of interactions resolved without escalation.
- Measurable CSAT lift vs. current agent-first baseline.

**Scope:**
- *In:* Self-service for benefits, coverage, claims, and billing questions.
- *Out:* Clinical judgment calls and claims disputes; full replacement of live agents.

**Risks / dependencies:**
- 50% resolution-rate target is flagged as aggressive for a first MVP, with no stated fallback plan if early SoCal data comes in lower.
- Depends on Feature 4 (Core Systems Integration) for underlying data.

**Design:** Formal design yet to come.

**Proof of tech / demo:** Formal proof of tech/demo yet to come.

**Questions:**
- What's the fallback plan or revised resolution-rate target if early SoCal data comes in below 50%?

---

## Feature 2: HIPAA-Compliant Personalization

**Feature ID:** TBD
**Status:** TBD

**Problem:**
Generic FAQ-matching chatbots can't deliver the differentiated, personalized support Optum needs; Companion must use member data to personalize responses, which requires compliant handling from day one.

**Background:**
Personalization uses member data and must be HIPAA-compliant by design, not retrofitted after the fact.

**Timing:** Launch target: Feb 2025 (Southern California) to meet MVP live deadline `[INFERRED: PRD gives one MVP date; no separate date for this sub-capability]`.

**Product requirements:**
- Personalize responses using member data.
- Build HIPAA compliance into the personalization flow from day one, not as a retrofit.

**Acceptance Criteria:**
- Given Companion accesses member data to personalize a response, When the response is generated, Then the data handling complies with HIPAA requirements by design (not added after launch).
- `[INFERRED — closest testable version]` Given a member with a benefits/claims history asks a question, When Companion responds, Then the response reflects that member's specific data rather than a generic templated answer.

**Value:** Healthcare-specific, compliant personalization is the stated differentiator vs. a generic chatbot layer, and underpins the CSAT and resolution-rate goals.

**Metrics:** No personalization-specific metric is stated in the PRD; contributes to overall CSAT lift `[INFERRED]`.

**Scope:**
- *In:* HIPAA-compliant use of member data to personalize responses.
- *Out:* No personalization-specific exclusion is stated in the PRD.

**Risks / dependencies:**
- Compliance-by-design requirement (Context section) — not retrofitted.
- Depends on Feature 4 (Core Systems Integration) for member data access.

**Design:** Formal design yet to come.

**Proof of tech / demo:** Formal proof of tech/demo yet to come.

**Questions:**
- What specific HIPAA compliance controls (e.g., data minimization, audit logging, access scoping) are required for this to be "by design"?
- The PRD doesn't define, in testable terms, what makes a response "healthcare-specific intelligence" vs. generic FAQ matching — what's the specific behavior to build/test against?

---

## Feature 3: Warm-Transfer Escalation

**Feature ID:** TBD
**Status:** TBD

**Problem:**
Complex queries that Companion can't resolve still need a human agent — today's handoffs typically force members to repeat themselves, and the PRD calls for this to instead reduce average handle time (AHT).

**Background:**
The escalation path is intended to lower AHT rather than simply deflect volume.

**Timing:** Launch target: Feb 2025 (Southern California) to meet MVP live deadline.

**Product requirements:**
- Route unresolved or complex queries in-app to live agents.
- Attach full conversational context via warm transfer so the agent starts from where Companion left off.

**Acceptance Criteria:**
- Given Companion cannot resolve a query, When it escalates, Then the query is routed in-app to a live agent.
- Given a query is escalated, When the agent receives it, Then full context is attached via warm transfer, and the member/provider does not need to repeat themselves.

**Value:** Reduces agent average handle time (AHT) by starting agents from context instead of a cold handoff, improving the experience for cases that still need a human.

**Metrics:** Expected impact on AHT is named as a tracked outcome for Support Operations; no specific target figure is stated in the PRD.

**Scope:**
- *In:* In-app routing to live agents for complex queries, with context passed via warm transfer.
- *Out:* Full replacement of live agents; clinical judgment calls and claims disputes remain agent-handled, not automated.

**Risks / dependencies:**
- Depends on Feature 4 (Core Systems Integration) to source the context passed at handoff.
- Feature 5 (Continuous Learning Loop) would consume escalation outcomes, but that loop is out of MVP scope.

**Design:** Formal design yet to come.

**Proof of tech / demo:** Formal proof of tech/demo yet to come.

**Questions:**
- No specific AHT reduction target is defined — what's the target metric/threshold for warm-transfer effectiveness?

---

## Feature 4: Core Systems Integration

**Feature ID:** TBD
**Status:** TBD

**Problem:**
Companion's core differentiation depends on deep integration with claims, benefits, and provider directory systems — without this, it's a generic chatbot layer, not a system that can actually resolve routine questions.

**Background:**
Flagged directly as a dependency risk: the Feb 2025 MVP timeline is tight given the number of required system integrations, and integration readiness needs confirmation from each owning team.

**Timing:** Launch target: Feb 2025 (Southern California) to meet MVP live deadline.

**Product requirements:**
- Integrate with claims systems.
- Integrate with benefits systems.
- Integrate with provider directory systems.

**Acceptance Criteria:**
- Given a member/provider question requires claims data, When Companion queries the claims system, Then it retrieves the data needed to answer.
- Given a member/provider question requires benefits data, When Companion queries the benefits system, Then it retrieves the data needed to answer.
- Given a member/provider question requires provider directory data, When Companion queries the provider directory system, Then it retrieves the data needed to answer.

**Value:** Named as Companion's core differentiator vs. a generic chatbot layer; enables both Self-Service Resolution (Feature 1) and HIPAA-Compliant Personalization (Feature 2).

**Metrics:** No integration-specific metric is stated in the PRD; contributes indirectly to the 50% resolution-rate goal `[INFERRED]`.

**Scope:**
- *In:* Integration with claims, benefits, and provider directory systems.
- *Out:* No systems beyond these three are named in the PRD.

**Risks / dependencies:**
- "MVP timeline (Feb 2025) is tight given the number of system integrations... integration readiness should be confirmed with each owning team" — named directly in PRD Risks.

**Design:** Formal design yet to come.

**Proof of tech / demo:** Formal proof of tech/demo yet to come.

**Questions:**
- What's the current integration-readiness status/timeline confirmation from each owning team (claims, benefits, provider directory)?

---

## Feature 5: Continuous Learning Loop — *(Out of MVP scope)*

**Feature ID:** TBD
**Status:** TBD

**Problem:**
The Recommendation states Companion should improve over time via continuous learning from resolved and escalated interactions, but this capability has no defined owner or feedback mechanism.

**Background:**
Named in the Recommendation, but **not listed under Scope's "In scope (MVP)" bullets** — treated here as a stated future capability, out of MVP scope, per PRD Risks: "Continuous learning loop needs an owner and a feedback mechanism... not yet specified."

**Timing:** No launch target is stated in the PRD `[INFERRED: not scheduled — not part of MVP scope]`.

**Product requirements:**
- Capture outcomes of resolved and escalated interactions as feedback.
- Use that feedback to improve Companion's performance over time.

**Acceptance Criteria:**
- `[INFERRED — closest testable version, mechanism undefined]` Given a query is resolved or escalated, When the interaction ends, Then the outcome is logged for future use in improving Companion.
- *(A full AC for "improves performance over time" cannot be written — see Questions.)*

**Value:** Supports ongoing improvement of resolution capability, which would help sustain progress toward the $30M/year by 2026 savings target `[INFERRED]`.

**Metrics:** None stated in the PRD.

**Scope:**
- *In:* Not part of MVP scope.
- *Out:* **Explicitly out of MVP scope** — absent from Section 6's "In scope (MVP)" list; confirmed by the PRD's own Risks section as unowned and unspecified.

**Risks / dependencies:**
- No owner assigned.
- No feedback mechanism defined.

**Design:** Formal design yet to come.

**Proof of tech / demo:** Formal proof of tech/demo yet to come.

**Questions:**
- Who owns the continuous learning loop, and what's the feedback mechanism for resolved/escalated interactions?
- Is this planned for a phase after MVP, and if so, when relative to the SoCal launch and the 2026 savings target?

---

## Cross-cutting Questions (from PRD Risks & Open Questions, not tied to a single feature)

- Savings trajectory ($5M post-MVP → $30M/year by 2026) implies multi-region rollout, but no timeline or scope for expansion beyond SoCal is defined in the PRD.
- No milestones are defined between MVP launch (Feb 2025) and the 2026 savings target.
