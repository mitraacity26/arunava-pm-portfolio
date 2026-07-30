# Companion — User Stories (v2, exhaustive AC coverage)
*Derived from: companion-feature-details.md | Audience: Dev team (sprint sizing) | Format: ID + Story Name + "As a... I want... so that..." + GWT AC | Priority: MoSCoW*
*AC coverage: happy path + failure/error, security/authorization, data integrity, audit/logging, performance, scope-boundary, and accessibility dimensions, per story, where applicable. Undefined specifics are tagged `TBD — Review Required` inline rather than dropped.*

---

## 1. Feature Overview

| Feature ID | Feature | Outcome it serves |
|---|---|---|
| F1 | Self-Service Resolution | Members/providers get instant answers without waiting for an agent |
| F2 | HIPAA-Compliant Personalization | Responses are relevant to the individual member, compliantly |
| F3 | Warm-Transfer Escalation | Agents resolve escalations faster (lower AHT) without re-asking the member |
| F4 | Core Systems Integration | Companion has the real data it needs to answer accurately — foundational to F1–F3 |
| F5 | Continuous Learning Loop *(out of MVP scope)* | Companion improves over time from resolved/escalated outcomes |

---

## F1 — Self-Service Resolution

Targets the highest-cost, lowest-complexity share of ticket volume by resolving routine benefits/coverage/claims/billing questions without an agent.

**F1-S1 — Instant Self-Service Answer for Member Query** — *Priority: Must*
As a **member**, I want to get an instant answer to a routine benefits/coverage/claims/billing question, so that I don't have to wait in queue for an agent.
- Given a member submits a routine benefits/coverage/claims/billing query, When Companion processes it, Then it returns a self-service answer without agent involvement.
- Given Companion has classified a query as routine and self-serviceable, When it generates the response, Then the response must be delivered within a latency threshold that supports an "instant" experience; specific SLA threshold is `TBD — Review Required`.
- Given a member submits a query in the explicitly excluded categories of clinical judgment calls or claims disputes, When Companion classifies it, Then it must not attempt self-service resolution and must route to a live agent (see F1-S4).
- Given a self-service response is delivered through the chat interface, When displayed, Then it must meet applicable accessibility standards for member-facing digital experiences; specific standards are `TBD — Review Required`.

**F1-S2 — Instant Self-Service Answer for Provider Query** — *Priority: Must*
As a **provider**, I want to get an instant answer to a routine support question, so that I don't have to wait in queue for an agent.
- Given a provider submits a routine support query, When Companion processes it, Then it returns a self-service answer without agent involvement.
- Given Companion has classified a provider query as routine and self-serviceable, When it generates the response, Then the response must be delivered within a latency threshold that supports an "instant" experience; specific SLA threshold is `TBD — Review Required`.
- Given a provider submits a query in the explicitly excluded categories of clinical judgment calls or claims disputes, When Companion classifies it, Then it must not attempt self-service resolution and must route to a live agent (see F1-S4).
- Given a self-service response is delivered through the chat interface, When displayed, Then it must meet applicable accessibility standards for provider-facing digital experiences; specific standards are `TBD — Review Required`.

**F1-S3 — Fallback Behavior on Triage/Resolution System Error** — *Priority: Must*
As a **member/provider**, I want Companion to handle system errors gracefully during triage or self-service resolution, so that I'm never left with an unhandled error and no path forward.
- Given a system error, integration failure, or unresolvable state occurs during triage or self-service resolution, When Companion encounters it, Then it must not present an unhandled error and must execute a defined fallback behavior, including in-app routing to a live agent where applicable; specific fallback behavior is `TBD — Review Required`.
- Given Companion cannot classify a submitted query as either routine/self-serviceable or complex/escalation-required, When classification is attempted, Then Companion must apply a defined classification fallback rather than leaving the query unhandled; the specific fallback logic is `TBD — Review Required` pending AI triage design confirmation.
- Given a fallback behavior is triggered, When the event is processed, Then it must be logged in a manner that supports operational reporting; exact log schema is `TBD — Review Required`.

**F1-S4 — Route Excluded Query Types to Live Agent** — *Priority: Must*
As a **member/provider**, I want queries involving clinical judgment calls or claims disputes to go straight to a live agent, so that I'm not given an automated answer to something requiring human judgment.
- Given a member or provider submits a query classified as a clinical judgment call or claims dispute, When Companion processes it, Then it must not attempt automated resolution and must route the interaction to a live agent.
- Given such a query is routed to a live agent, When escalation is triggered, Then full prior conversation context must be attached via the warm-transfer mechanism (see F3-S2) so the user doesn't repeat themselves.
- Given Companion is operating under the SoCal MVP scope, When a query is submitted from outside the SoCal geography, Then Companion's behavior is `TBD — Review Required` pending MVP boundary enforcement design.

**F1-S5 — Log Interaction Outcomes for Resolution Rate & CSAT Measurement** — *Priority: Must*
As a **support operations manager**, I want every Companion interaction's resolution/escalation outcome logged, so that I can measure the 50% self-service resolution rate and CSAT lift against the agent-first baseline.
- Given Companion resolves or escalates an interaction, When the outcome is determined, Then it must be logged in a manner that supports measurement of the self-service resolution rate against the 50% target.
- Given logged outcomes, When aggregated, Then they must support CSAT lift measurement against the agent-first baseline.
- `[INFERRED — carried from source]` No fallback plan or revised target is defined if early SoCal resolution rate comes in below 50%; decision path is `TBD — Review Required`.

**Dependencies:** F4 (Core Systems Integration) for underlying data. F3 (Warm-Transfer Escalation) for the mechanics of any escalation triggered here — see F1-S4 cross-reference.

**Out of scope:** Clinical judgment calls and claims disputes (self-service attempt); full replacement of live agents.

---

## F2 — HIPAA-Compliant Personalization

Personalizes responses using member data, with compliance built in rather than added later — the stated differentiator vs. a generic FAQ bot.

**F2-S1 — Personalized Response from Member Data** — *Priority: Must*
As a **member**, I want my responses personalized using my own data retrieved from UHG systems of record, so that I get answers relevant to my actual coverage/history instead of a generic template.
- Given an authenticated member submits a benefits/coverage/claims/billing query, When Companion responds, Then the response must be personalized using that member's data retrieved from integrated UHG systems of record, not a generic or static response.
- Given Companion generates a personalized response, When it does so, Then the response must be derived exclusively from authoritative retrieved data; Companion must not fabricate, infer, or substitute member-specific values not present in the retrieved payload.
- Given personalization data is retrieved, When the response is generated, Then retrieval and application must not introduce latency that degrades the instant self-service experience; specific latency threshold is `TBD — Review Required`.
- Given a personalized response is delivered through the chat interface, When displayed, Then it must meet applicable accessibility standards for member-facing digital experiences; specific standards are `TBD — Review Required`.

**F2-S2 — Personalized Response from Provider Context Data** — *Priority: Must*
As a **provider**, I want my responses personalized using data relevant to my support context retrieved from UHG systems of record, so that I get answers relevant to my actual situation instead of a generic template.
- Given an authenticated provider submits a support query, When Companion responds, Then the response must be personalized using data relevant to that provider's context retrieved from integrated UHG systems of record, not a generic or static response.
- Given Companion generates a personalized response for a provider, When it does so, Then the response must be derived exclusively from authoritative retrieved data; Companion must not fabricate, infer, or substitute values not present in the retrieved payload.
- Given personalization data is retrieved for a provider query, When the response is generated, Then retrieval and application must not introduce latency that degrades the instant self-service experience; specific latency threshold is `TBD — Review Required`.
- Given a personalized response is delivered through the chat interface, When displayed, Then it must meet applicable accessibility standards for provider-facing digital experiences; specific standards are `TBD — Review Required`.

**F2-S3 — Fallback When Personalization Data Is Unavailable** — *Priority: Must*
As a **member/provider**, I want Companion to apply a defined fallback when my data can't be retrieved for personalization, so that I'm never shown a response based on incomplete or fabricated data.
- Given member/provider data required for personalization cannot be retrieved due to integration failure or unavailability, When Companion detects this, Then it must apply a defined fallback behavior and must not generate a personalized response from incomplete data; specific fallback behavior is `TBD — Review Required`.
- Given a query spans multiple data domains and only some retrieve successfully, When Companion evaluates completeness, Then it must not generate a partial personalized response using only the successfully retrieved domains — the fallback applies to the entire interaction.
- Given a fallback is triggered, When the event is processed, Then it must be logged, capturing session identifier, data domain, retrieval status, and timestamp, to support HIPAA audit requirements.

**F2-S4 — Enforce HIPAA-Compliant Access Controls on Personalization Data** — *Priority: Must*
As a **compliance officer**, I want access to member data within personalization restricted to authorized system components only, so that Companion's data handling is compliant by design, not retrofitted.
- Given the personalization flow accesses member data, When any system component requests it, Then access must be restricted exclusively to authorized components (Member Data Access Layer, Personalization Engine); requests from unauthorized components must be denied.
- Given an unauthorized access attempt occurs, When detected, Then it must be blocked and no member data returned to the requestor; internal system error details must not be exposed.
- Given member data is used during a personalization transaction, When the transaction concludes, Then the data must not be retained, cached, or persisted beyond the transaction scope in any component not explicitly authorized to hold it; specific retention boundaries are `TBD — Review Required`.

**F2-S5 — Log Member Data Access Events for HIPAA Audit** — *Priority: Must*
As a **compliance officer**, I want every member data access event during personalization logged, so that Companion can demonstrate full auditability to regulators.
- Given any authorized component accesses member data, When the access event completes (success, failure, timeout, or denial), Then it must be recorded in an audit log; no access event may be omitted regardless of outcome.
- Given a log entry is written, When captured, Then it must include requesting component identity, session identifier, data domain, system of record, timestamp, and access outcome; log retention policy is `TBD — Review Required`.
- Given a logging failure occurs, When detected, Then it must be flagged as a compliance anomaly requiring investigation rather than silently dropped.

**F2-S6 — Scope Personalized Response Content to Authorized Data Only** — *Priority: Must*
As a **compliance officer**, I want personalized responses to contain only the data needed to answer the specific query, so that no member data is exposed beyond the intended response.
- Given Companion assembles a personalized response, When it does so, Then the response must contain only the data values required to answer the specific query — no additional retrieved data included.
- Given a response is delivered, When it reaches the chat interface, Then no member data may be surfaced to unauthorized system components, third-party services, or end-user interfaces beyond the authenticated session.
- Given a response fails this exposure-boundary check, When detected, Then it must not be delivered, and the violation must be logged and escalated as a compliance anomaly.

**Dependencies:** F4 (Core Systems Integration) for member data access.

**Out of scope:** None stated in the source — flagged, not assumed.

---

## F3 — Warm-Transfer Escalation

Routes queries Companion can't resolve to a live agent in-app, with full context attached, aimed at reducing AHT rather than just deflecting volume.

**F3-S1 — Route Unresolved Query to Live Agent In-App** — *Priority: Must*
As a **member/provider** whose issue Companion can't resolve, I want to be routed to a live agent without leaving the app, so that I don't have to start over somewhere else.
- Given Companion cannot resolve a query, When it escalates, Then the query must be routed in-app to a live agent.
- Given the in-app escalation experience is presented, When displayed, Then it must meet applicable accessibility standards for member/provider-facing digital experiences; specific standards are `TBD — Review Required`.

**F3-S2 — Deliver Full Conversation Context via Warm Transfer** — *Priority: Must*
As a **support agent**, I want to receive the full prior conversation context on an escalated case, so that I don't have to make the member/provider repeat themselves and can resolve faster.
- Given a query is escalated, When the agent receives it, Then full prior conversation context must be attached via warm transfer, and the member/provider must not need to repeat information already provided.
- Given context is packaged for transfer, When transmitted, Then it must be a complete and accurate representation of the prior interaction, with no messages, query details, or user-provided information omitted, truncated, or altered.
- Given the agent reviews the transferred context, When they do so, Then it must be presented in a format that is actionable and sufficient to continue resolution without re-triage.

**F3-S3 — Fallback When Warm-Transfer Context Delivery Fails** — *Priority: Must*
As a **member/provider** being escalated, I want Companion to handle a failed context handoff gracefully, so that I'm not silently dropped without a resolution path.
- Given warm-transfer context delivery fails due to a system error, transmission failure, or agent routing unavailability, When this occurs, Then Companion must execute a defined fallback behavior and must not silently drop the escalation; specific fallback behavior is `TBD — Review Required`.

**F3-S4 — Log Escalation & Handoff Events for AHT/CSAT Measurement** — *Priority: Must*
As a **support operations manager**, I want escalation and warm-transfer events logged, so that I can measure AHT reduction and CSAT lift for escalated interactions relative to the agent-first baseline.
- Given an escalation and warm-transfer handoff completes, When the event is processed, Then it must be logged, capturing the escalation event, context transfer outcome, and handoff completion status; no event may be omitted.
- Given logged escalation data, When aggregated, Then it must support measurement of AHT reduction relative to the current agent-first baseline and contribution to CSAT lift; specific AHT target is `TBD — Review Required` (no figure stated in source).

**F3-S5 — Enforce HIPAA Compliance on Transferred Context Data** — *Priority: Must*
As a **compliance officer**, I want all data in the warm-transfer context handled per HIPAA requirements, so that no unauthorized exposure occurs during handoff.
- Given member/provider data is included in transferred context, When transmitted, Then it must be handled in strict compliance with HIPAA requirements, with no unauthorized exposure to system actors or agents outside the scope of the authorized escalation.

**Dependencies:** F4 (Core Systems Integration) for context data sourcing. F5 (Continuous Learning Loop) would consume escalation outcomes, but that loop is out of MVP scope.

**Out of scope:** Full replacement of live agents; clinical judgment calls and claims disputes remain agent-handled (routed via F1-S4, not re-litigated here).

---

## F4 — Core Systems Integration

Foundational integration with claims, benefits, and provider directory systems — without it, Companion can't answer accurately or personalize.

**F4-S1 — Retrieve Real-Time Claims Data for Self-Service Queries** — *Priority: Must*
As a **member/provider**, I want Companion to pull accurate claims data in real time, so that I get a correct, up-to-date answer without contacting an agent.
- Given a member/provider question requires claims data, When Companion queries the claims system, Then it must retrieve the relevant data in real time and use it as the basis for the response, not static or generic content.
- Given data is returned from the claims system, When used to generate a response, Then it must be sourced exclusively from the authoritative claims system of record; Companion must not substitute inferred or fabricated values when authoritative data isn't returned.

**F4-S2 — Retrieve Real-Time Benefits Data for Self-Service Queries** — *Priority: Must*
As a **member/provider**, I want Companion to pull accurate benefits data in real time, so that I get a correct, up-to-date answer without contacting an agent.
- Given a member/provider question requires benefits data, When Companion queries the benefits system, Then it must retrieve the relevant data in real time and use it as the basis for the response, not static or generic content.
- Given data is returned from the benefits system, When used to generate a response, Then it must be sourced exclusively from the authoritative benefits system of record; Companion must not substitute inferred or fabricated values when authoritative data isn't returned.

**F4-S3 — Retrieve Real-Time Provider Directory Data for Self-Service Queries** — *Priority: Must*
As a **member/provider**, I want Companion to pull accurate provider directory data in real time, so that I get a correct, up-to-date answer without contacting an agent.
- Given a member/provider question requires provider directory data, When Companion queries the provider directory, Then it must retrieve the relevant data in real time and use it as the basis for the response, not static or generic content.
- Given data is returned from the provider directory, When used to generate a response, Then it must be sourced exclusively from the authoritative provider directory of record; Companion must not substitute inferred or fabricated values when authoritative data isn't returned.

**F4-S4 — Fallback on Integration Failure Across Claims/Benefits/Provider-Directory** — *Priority: Must*
As a **member/provider**, I want Companion to handle integration failures gracefully, so that I'm never given a response based on missing or fabricated system data.
- Given a real-time data retrieval request to the claims system, benefits system, or provider directory fails due to a transient error, timeout, or system unavailability, When this occurs, Then Companion must execute the defined fallback behavior for that integration and must not generate a response from incomplete or missing data; specific fallback behavior per integration is `TBD — Review Required`.

**F4-S5 — Log Data Retrieval Events & Track Integration Readiness** — *Priority: Must*
As a **compliance officer / engineering lead**, I want all data retrieval events logged and integration readiness tracked ahead of MVP launch, so that HIPAA audit requirements are met and the Feb 2025 dependency risk stays visible.
- Given Companion retrieves data from any of the three integrated systems, When the retrieval occurs, Then the event must be logged in a manner that supports HIPAA audit requirements; no retrieval event may be omitted.
- Given the February 2025 SoCal MVP delivery date, When integration readiness is assessed for the claims system, benefits system, and provider directory, Then readiness must be confirmed with each owning team prior to launch; any unconfirmed readiness must be escalated as a dependency risk.

**Dependencies:** None upstream — this is the foundational feature F1, F2, and F3 depend on. Carried risk from source: MVP timeline is tight given the number of integrations; readiness not yet confirmed with each owning team.

**Out of scope:** No systems beyond claims, benefits, and provider directory are named in the source.

---

## F5 — Continuous Learning Loop *(Out of MVP scope)*

Named in the source Recommendation but not part of MVP scope; no owner or feedback mechanism defined yet.

**F5-S1 — Log Resolved/Escalated Outcomes for Future Learning Use** — *Priority: Won't (this release)*
As a **product/ops owner**, I want resolved and escalated interaction outcomes logged, so that they can later be used to improve Companion's performance.
- `[INFERRED — carried from source; mechanism undefined]` Given a query is resolved or escalated, When the interaction ends, Then the outcome must be logged for future use in improving Companion; the specific ingestion/model-update mechanism is `TBD — Review Required`.
- *A full story/AC for "improves performance over time" cannot be written — no owner or feedback mechanism is defined. See Open Questions.*

**Dependencies:** None defined. No owner assigned (carried from source).

**Out of scope:** The entire feature is out of MVP scope.

---

## 2. Open Questions

Reserved for gaps that block writing *any* testable AC at all (per-AC parameter gaps are tagged inline as `TBD — Review Required` above and aren't repeated here):

- **F1:** No fallback plan or revised target is defined if early SoCal resolution rate comes in below 50%.
- **F1/F4:** No MVP geographic-boundary enforcement behavior is defined for queries submitted from outside SoCal.
- **F2:** "Healthcare-specific intelligence" vs. generic FAQ matching isn't defined in testable terms beyond "uses member data."
- **F3:** No specific AHT reduction target/threshold is defined for warm-transfer effectiveness.
- **F4:** Integration-readiness status/timeline with each owning team (claims, benefits, provider directory) is not yet confirmed.
- **F5:** No owner or feedback mechanism is defined at all — F5-S1 is the closest testable placeholder, not a complete solution. Timing relative to MVP is also undefined.
