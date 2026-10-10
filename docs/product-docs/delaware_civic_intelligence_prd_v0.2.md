# Delaware Civic Intelligence Platform
## Product Requirements Document

**Status:** Draft for product and engineering review  
**Version:** 0.2  
**Last updated:** October 9, 2026  
**Initial market:** Delaware  
**Primary audience:** Delaware residents  
**Product type:** Public civic-information platform  
**Working product name:** Delaware Civic Intelligence Platform

---

## 0. Revision Notes

Version 0.2 converts the original concept document into a more implementation-ready PRD.

Key changes from v0.1:

1. **Narrowed the MVP.** The first release is explicitly Delaware state legislative intelligence. Meetings, regulations, spending, lobbying, campaign finance, and municipal government remain planned extensions.
2. **Separated fact from interpretation more rigorously.** "Why it matters" is replaced by **What changes** and **Potential practical effects**, with stronger provenance requirements.
3. **Made "What happens next?" deterministic where possible.** Legislative procedure should be generated from structured state and chamber rules rather than free-form model prediction.
4. **Added source-of-truth rules.** The platform must distinguish official government records, structured transformations, AI-generated explanations, and third-party reporting.
5. **Added data coverage and freshness behavior.** The UI must expose stale, missing, delayed, or incomplete source data rather than silently guessing.
6. **Added functional requirements and acceptance criteria.**
7. **Added AI quality gates, fallback behavior, and confidence rules.**
8. **Added privacy, accessibility, security, observability, analytics, and launch requirements.**
9. **Added explicit dependencies, assumptions, risks, and unresolved product decisions.**
10. **Added a Delaware source verification appendix.** Current public sources support the strategy, but implementation discovery is still required for interfaces without a documented public API.

---

# 1. Executive Summary

Government produces a large amount of public information, including legislation, amendments, roll-call votes, committee actions, public meetings, regulations, fiscal notes, budgets, lobbying disclosures, campaign-finance records, contracts, and expenditures.

The primary problem is not simply that this information is unavailable.

The problem is that it is:

- fragmented across government systems,
- written for legal or administrative audiences,
- organized around government processes rather than citizen questions,
- difficult to connect across agencies and stages of government,
- difficult to monitor over time,
- and often discovered only after the most useful opportunity for citizen participation has passed.

Citizens generally do not think in terms of:

- bill numbers,
- legislative sessions,
- administrative codes,
- committee calendars,
- agency structures,
- appropriations,
- regulatory dockets,
- or government jurisdictions.

They think in terms of questions such as:

- What is the government doing about housing?
- Why are my electric rates changing?
- What would this bill actually change?
- Did this proposal become law?
- Who voted for it?
- Can I still influence this decision?
- Who is responsible for this issue?
- What happened after this law passed?
- Was the program actually implemented?
- How much did it cost?
- Who do I contact?
- What meetings should I pay attention to?

The Delaware Civic Intelligence Platform will transform public-facing government information into a connected, source-backed civic information system.

The initial product will help residents:

1. discover relevant legislation,
2. understand what it would change,
3. follow its current status and history,
4. understand what happens next,
5. inspect amendments and votes,
6. identify known participation opportunities,
7. and verify every important claim against primary sources.

The long-term product vision is a **Civic Knowledge Graph** connecting:

**People → Offices → Districts → Committees → Bills → Amendments → Votes → Meetings → Regulations → Agencies → Budgets → Contracts → Expenditures → Lobbying → Organizations**

The durable product advantage should not be "AI bill summaries." Summarization is a capability. The differentiated product is the continuously maintained set of relationships connecting government decisions, procedures, participation opportunities, implementation obligations, and public money.

---

# 2. Product Vision

## 2.1 Vision

Make government activity understandable, traceable, and actionable for ordinary citizens.

## 2.2 Product promise

A resident should be able to answer:

> **What is happening, what changes, who controls it, what happens next, and what can I do?**

without needing to understand the internal structure of government first.

## 2.3 Long-term aspiration

Become the public-facing intelligence layer between citizens and government records.

The platform should eventually function as a living map of how government decisions are:

1. proposed,
2. debated,
3. changed,
4. approved,
5. implemented,
6. funded,
7. and carried out.

---

# 3. Product Thesis

Public government data already contains much of the information citizens need.

What is missing is infrastructure that connects those records into an understandable and trustworthy narrative.

The platform should transform isolated government documents into a continuously updated model of:

**What government is considering**  
→ **What changed**  
→ **Who decides**  
→ **When the public can act**  
→ **What government decided**  
→ **What government was required to do**  
→ **Whether it actually happened**

That lifecycle—not generic AI summarization—is the core product.

---

# 4. Problem Statement

## 4.1 Fragmentation

Relevant records frequently live across different systems.

For a single policy issue, a citizen may need to inspect:

- General Assembly legislation,
- committee records,
- amendments,
- roll-call votes,
- fiscal notes,
- public meeting calendars,
- agency websites,
- proposed regulations,
- final regulations,
- budget documents,
- expenditure databases,
- lobbying disclosures,
- and local-government records.

The user is currently responsible for connecting these records mentally.

The platform should make those connections explicit.

## 4.2 Government information lacks context

A government website may accurately report:

> HB 123 — Assigned to House Administration Committee.

That information is technically correct but incomplete for most citizens.

A citizen may also need to know:

- What would HB 123 change?
- Is committee assignment routine or a meaningful decision point?
- Is a hearing scheduled?
- Can the public attend or testify?
- Who sits on the committee?
- What can happen after committee consideration?
- Has the proposal changed since introduction?
- Is there a known upcoming opportunity to participate?

The platform must provide context alongside facts.

## 4.3 Legal and procedural language creates comprehension barriers

Legislation and regulations are optimized for legal precision, not general comprehension.

Citizens often need:

- plain-language explanations,
- definitions,
- examples,
- comparisons,
- procedural explanations,
- and distinctions between current law and proposed law.

The platform should provide this interpretation without obscuring the underlying source material.

## 4.4 Citizens learn about decisions too late

Most civic tools are optimized for retrospective lookup.

They tell users:

> A vote occurred.

The more valuable information may be:

> A hearing is scheduled Tuesday, and written comments are due Monday.

The product should emphasize **future decision points and participation opportunities** where authoritative data supports them.

## 4.5 Government accountability becomes difficult after legislation passes

Traditional bill-tracking systems often treat enactment as the end state.

For citizens, enactment frequently begins a new process.

After passage:

- regulations may need to be written,
- agencies may need to implement programs,
- funding may need to be appropriated,
- contracts may need to be awarded,
- deadlines may need to be met,
- fees may need to be established,
- reports may be due,
- and enforcement may begin months or years later.

The product should eventually track the transition from:

**law → implementation requirement → government action → observable outcome**

## 4.6 Citizens think in problems, not jurisdictions

A resident with a road, zoning, school, tax, utility, or licensing problem often does not know whether responsibility belongs to:

- a municipality,
- county,
- school district,
- state agency,
- legislature,
- executive branch,
- or federal government.

Future releases should route a citizen's real-world question to the responsible government entity and process.

---

# 5. Product Goals

## G1 — Improve comprehension

Allow a citizen with no legislative expertise to understand a government action quickly and accurately.

## G2 — Improve discovery

Help citizens discover government activity relevant to concepts and topics they care about, not only bill numbers.

## G3 — Improve procedural understanding

Explain where an issue currently sits in the process and what procedural steps are possible next.

## G4 — Improve civic participation

Surface verified opportunities to:

- attend,
- comment,
- testify,
- contact relevant officials,
- or otherwise participate.

## G5 — Increase transparency

Make government records easier to connect, inspect, compare, and monitor over time.

## G6 — Establish trustworthy AI-assisted civic information

Use AI to explain public records while preserving provenance, uncertainty, and a clear path to the primary source.

## G7 — Build reusable civic data infrastructure

Create normalized entities and relationships that support future capabilities beyond bill summaries.

---

# 6. Non-Goals

The initial product will not attempt to:

- advocate for political positions,
- tell users how they should vote,
- assign ideological ratings,
- label bills as "good" or "bad,"
- infer lawmakers' motives,
- predict individual votes,
- predict legislative outcomes as facts,
- infer corruption or improper influence,
- replace official government records,
- provide legal advice,
- become a social network,
- host unmoderated political discussion,
- cover all U.S. states,
- provide complete municipal coverage,
- provide comprehensive campaign-finance analysis,
- provide comprehensive lobbying analysis,
- measure long-term real-world policy outcomes,
- or automatically determine that correlation between money, lobbying, sponsorship, or voting establishes causation.

---

# 7. Product Principles

## 7.1 Source first

Every substantive factual claim presented by the platform must be traceable to a source record or a clearly identified structured transformation of source records.

## 7.2 Explain, do not editorialize

The system should make complexity understandable without inserting political judgment.

## 7.3 Separate fact from interpretation

Content must distinguish among:

### Official fact
Directly supported by an authoritative source.

### Structured derivation
Computed deterministically from official records.

Examples:

- vote totals,
- days until a hearing,
- whether a bill changed versions,
- whether an implementation deadline has passed.

### Plain-language interpretation
An explanation of what sourced text means.

### Attributed position
A position explicitly stated by a legislator, agency, organization, witness, journalist, or other party.

### Potential practical effect
A reasonable implication that goes beyond direct statutory wording and therefore must be labeled as analysis and supported by evidence.

### Unknown / uncertain
A question the platform cannot answer reliably from available evidence.

These categories must not be presented interchangeably.

## 7.4 Prefer "unknown" to invented certainty

If the source data does not support a conclusion, the platform should say so.

Examples:

> No public hearing is currently identified in the data we have.

is preferable to:

> There is no hearing.

Similarly:

> We have not identified an implementation record.

is preferable to:

> The agency has not implemented the law.

## 7.5 Show the process

The platform should explain government procedure rather than merely display statuses.

## 7.6 Optimize for action

When supported by evidence, every active issue should answer:

> **What happens next?**

and:

> **Is there a known opportunity to participate?**

## 7.7 Progressive disclosure

Users should be able to understand an issue in approximately 30–90 seconds and then drill into details and primary sources.

## 7.8 Neutrality by design

Neutrality should be reinforced through:

- standardized templates,
- symmetric metadata,
- primary-source citation,
- neutral ordering rules,
- visible attribution,
- consistent terminology,
- and correction mechanisms.

Model prompting alone is not an adequate neutrality strategy.

## 7.9 Current version first

When legislation has changed, the product should default to the current operative version while preserving a clear history of prior versions.

## 7.10 Public records remain authoritative

The platform is an interpretation and navigation layer.

Official government records remain the legal source of truth.

---

# 8. Target Users

## Persona 1 — Interested citizen

### Description
A resident who follows local news occasionally but does not understand legislative procedure.

### Needs
- Understand what a bill changes.
- Determine whether it matters to them.
- Understand what happens next.
- See how representatives voted.
- Know whether a participation opportunity exists.

## Persona 2 — Issue-focused citizen

### Description
A resident particularly interested in topics such as:

- education,
- development,
- healthcare,
- taxes,
- environment,
- firearms,
- housing,
- utilities,
- transportation,
- or criminal justice.

### Needs
- Follow topics rather than bill numbers.
- Discover meaningful changes.
- Find upcoming meetings and regulatory events.
- Track an issue across government bodies.

## Persona 3 — Journalist / content creator

### Description
Someone producing public-facing reporting, newsletters, videos, social posts, or civic content.

### Needs
- Discover developments quickly.
- Verify statements against primary sources.
- Compare bill versions.
- Find votes and amendments.
- identify upcoming hearings.
- deep-link to authoritative records.

## Persona 4 — Civic organization

### Description
A nonprofit, advocacy group, neighborhood group, business group, or community organization.

### Needs
- Monitor relevant legislation.
- identify participation deadlines.
- follow committees and agencies.
- share understandable, sourced information with members.

## Persona 5 — Citizen with a specific problem

### Description
A resident who does not consider themselves politically engaged but has a concrete issue.

Examples:

- road condition,
- zoning proposal,
- utility issue,
- school policy,
- property tax,
- licensing requirement.

### Needs
Determine:

- which level of government controls the issue,
- which organization is responsible,
- what process governs the issue,
- who represents them,
- and how to intervene.

This persona becomes increasingly important as the product expands into local government.

---

# 9. Core User Jobs

## Understand

> Explain what this bill would change.

## Discover

> What is happening in Delaware government related to housing?

## Compare

> What changed in the newest amendment or substitute?

## Follow process

> Where is this bill right now?

## Anticipate

> What can happen next?

## Participate

> Is there an upcoming hearing, comment deadline, or other way to participate?

## Attribute

> Who introduced this, who sits on the committee, and how did legislators vote?

## Research

> Show me the official evidence behind this explanation.

## Monitor

> Tell me when something materially changes.

## Connect

> Is this regulation implementing a law passed earlier?

## Investigate implementation

> This law passed six months ago. What implementation actions were required, and which have public evidence of completion?

---

# 10. Scope Strategy

The product should deliberately expand by **government lifecycle**, not by accumulating disconnected datasets.

## Phase 1 — Legislative intelligence

**Understand what government is considering.**

Includes:

- legislative search,
- bill detail,
- current status,
- timeline,
- sponsors,
- committees,
- votes,
- versions,
- amendments/substitutes,
- fiscal-note information,
- source-backed explanations,
- "What happens next?"

## Phase 2 — Civic action

**Understand and participate before decisions are complete.**

Adds:

- public meetings,
- agendas,
- hearing matching,
- known participation mechanisms,
- subscriptions,
- notifications,
- topic feeds.

## Phase 3 — Implementation intelligence

**Understand how enacted policy becomes operational.**

Adds:

- proposed/final regulations,
- statutory implementation obligations,
- deadlines,
- responsible agencies,
- public-comment windows,
- implementation milestones.

## Phase 4 — Accountability graph

**Connect decisions to public resources and influence records.**

Adds:

- budgets,
- appropriations,
- contracts,
- expenditures,
- lobbying disclosures,
- campaign-finance records.

## Phase 5 — Local government

**Apply the model to everyday government.**

Adds:

- county government,
- municipalities,
- school boards,
- planning and zoning,
- local ordinances,
- local budgets,
- Government Responsibility Router.

---

# 11. MVP Definition

The MVP is **Phase 1: Delaware state legislative intelligence**.

The MVP is not required to launch with:

- public meeting ingestion,
- regulations,
- notifications,
- user accounts,
- personalized districts,
- lobbying,
- campaign finance,
- spending,
- municipal government,
- AI chat,
- or policy-outcome tracking.

These should not delay validation of the core legislation experience.

## 11.1 MVP user outcome

A user who arrives with only a bill number, policy phrase, or topic should be able to:

1. find the relevant bill,
2. understand what the current version changes,
3. understand where the bill is in the process,
4. understand the procedural possibilities that follow,
5. inspect significant version changes,
6. see sponsorship and recorded votes,
7. inspect fiscal information where available,
8. and verify the explanation using primary sources.

---

# 12. MVP Functional Requirements

## FR-1 — Legislative search

Users must be able to search by:

- bill number,
- keyword,
- topic,
- sponsor,
- bill title,
- phrase,
- and natural-language concept.

Examples:

- `HB 350`
- `hospital assessment`
- `housing`
- `bills introduced by Senator X`
- `property tax relief`

### Requirements

- Exact bill-number matches should rank first.
- Current-session legislation should be distinguishable from historical legislation.
- Search must expose zero-result states clearly.
- Semantic results must not imply exact textual matches where none exist.
- Each result must show enough context to distinguish similar bills.

### MVP acceptance criteria

- A valid current-session bill number returns the matching bill as the top result.
- Keyword search returns bills containing or strongly related to the requested concept.
- Search result cards show bill number, title/short description, current status, and last material action date.
- Historical results, if included, are visibly labeled with their session.

---

## FR-2 — Bill header and identity

Each bill page must display:

- bill number,
- General Assembly/session,
- chamber/origin,
- official title,
- current status,
- introduced date,
- primary sponsor,
- latest material action,
- effective date when known,
- current-version indicator,
- source freshness timestamp.

### Acceptance criteria

- Core identity fields come from structured source records, not model generation.
- Missing fields are displayed as unavailable rather than fabricated.
- The bill's current session and current version are unambiguous.

---

## FR-3 — Plain-language explanation

Each eligible bill should contain a concise explanation answering:

> **What would this bill change?**

Target reading time:

**30–60 seconds**

### Requirements

- Explanation must be grounded in the current operative bill text and official synopsis where available.
- The system must not describe introduced language as current if it has been superseded.
- The explanation should distinguish existing law from proposed changes where the source makes this determinable.
- Material qualifications, exemptions, thresholds, dates, and exceptions should not be omitted merely to simplify the summary.

### Acceptance criteria

- Each substantive summary statement retains source provenance.
- The user can reveal supporting source material.
- A bill with insufficient machine-readable source content receives a reduced or withheld summary rather than an invented one.
- Summary generation can be re-run when the operative version changes.

---

## FR-4 — Key provisions

The product should break complex legislation into major provisions.

Example:

**The bill would:**

1. create X,
2. require Y,
3. authorize Z,
4. change the effective date of Q.

### Requirements

- Key provisions must map to current bill text.
- The feature must not inflate minor technical drafting changes into major policy provisions.
- Repeals and changed definitions should be surfaced when materially important.

---

## FR-5 — Potentially affected groups

Where evidence supports it, the product may display structured categories such as:

- homeowners,
- renters,
- teachers,
- healthcare providers,
- businesses,
- state agencies,
- drivers,
- municipalities.

### Requirements

This feature must distinguish:

**Explicitly affected entities**  
Named directly in the legislation.

from:

**Potentially affected groups**  
Inferred from the operation of the legislation.

Inferred groups require a short explanation of the connection and should not be shown if confidence is low.

---

## FR-6 — Legislative timeline

Each bill must expose a chronological timeline of known events.

Potential events include:

- introduced,
- assigned/reassigned to committee,
- hearing or meeting activity,
- committee action,
- amendment filed,
- amendment adopted/rejected,
- substitute introduced,
- floor vote,
- transmitted to other chamber,
- governor action,
- signed,
- vetoed,
- session law publication,
- effective date.

Each timeline event should contain:

- date,
- official action,
- plain-language explanation where useful,
- source.

### Acceptance criteria

- Timeline order is deterministic.
- Official action text remains available.
- AI is not used to invent intermediate events.
- Duplicate source events are de-duplicated without deleting materially distinct actions.

---

## FR-7 — "What happens next?"

This is a core differentiating feature.

Every active piece of legislation should answer:

> **What procedural steps are possible next?**

### Requirements

The feature should be rules-driven wherever possible.

Example:

**Current state:** Assigned to Senate Judiciary Committee

**Possible next step:** The committee may consider the bill and may report it to the Senate.

### Important constraint

The platform should explain **procedure**, not predict **political outcome**.

Avoid:

> The bill will probably pass.

Prefer:

> If the committee reports the bill, it may advance to consideration by the full Senate.

### Acceptance criteria

- Output maps to a known bill state.
- Output does not claim a future event is scheduled unless an authoritative source identifies it.
- Unsupported procedural states fall back to a generic explanation rather than hallucinated steps.
- Terminal states such as signed, vetoed, defeated, or expired have state-appropriate explanations.

---

## FR-8 — Participation opportunity

The platform should answer:

> **Is there a known public participation opportunity associated with this issue right now?**

The MVP may have limited capability here until meeting data is integrated.

### MVP behavior

For Phase 1:

- Link to known official contact information or hearing information only when the legislative source directly exposes it.
- Do not manufacture generic "take action" prompts.
- Clearly state that meeting and hearing coverage will become more complete when Phase 2 sources are integrated.

### Phase 2 behavior

Potential opportunities include:

- committee hearing,
- public meeting,
- testimony,
- written comment,
- regulatory comment,
- upcoming vote,
- official contact path.

### Language rule

Prefer:

> No current participation opportunity was identified in our available sources.

over:

> There are no participation opportunities.

---

## FR-9 — Sponsors and legislators

Users should be able to inspect:

- primary sponsor,
- additional sponsors/co-sponsors,
- chamber,
- district,
- party where officially available,
- official profile/contact link.

Later releases may add:

- committee memberships,
- sponsorship patterns,
- historical voting analysis.

---

## FR-10 — Voting records

Where a roll call exists, display:

- chamber,
- vote date,
- motion/vote type if available,
- result,
- Yes,
- No,
- Absent,
- Not Voting or equivalent source categories.

### Acceptance criteria

- Vote totals must be computed from or match official structured/primary-source records.
- The system should detect disagreement between computed totals and displayed official totals and flag the record for review.
- Individual vote records must not be generated from summaries.

---

## FR-11 — Version and amendment intelligence

The product must understand that a bill can change materially.

Possible source document types include:

- introduced bill,
- amendment,
- substitute,
- engrossed/final bill,
- enrolled bill,
- session law.

### User experience

Users should be able to answer:

- What is the current version?
- What changed?
- When did it change?
- Which amendment or substitute caused the change?

### Requirements

AI may explain differences, but the underlying diff must be derived from identified source versions.

### Acceptance criteria

- Current-version identity is known before a "current bill" summary is generated.
- The platform never presents a previous version as current without a warning.
- Meaningful changes can be traced to source text.
- Additions, deletions, changed numbers, dates, eligibility rules, exemptions, authority, enforcement, and funding should receive particular attention.

---

## FR-12 — Fiscal information

Where an official fiscal note or fee-impact record exists, display:

- presence/status of fiscal note,
- source link,
- government cost or revenue estimate where extractable,
- affected agency where identified,
- relevant fiscal years where identified.

### Requirements

- Monetary amounts should receive deterministic validation.
- If the source only says a fiscal note exists, the platform must not fabricate the financial conclusion.
- "No fiscal note" must not be interpreted as "no cost."

---

## FR-13 — Source transparency

Every AI-generated substantive explanation must retain provenance.

At minimum, provenance should include:

- source URL,
- source type,
- source document identifier where available,
- source version,
- retrieval timestamp,
- relevant text span or section,
- generation version/model metadata internally.

### User experience

The user should be able to select something equivalent to:

> **View source**

or:

> **Why am I seeing this?**

and reach the supporting primary record.

---

## FR-14 — Topic classification

Bills should receive standardized topic labels.

Initial taxonomy may include:

- Agriculture
- Business
- Civil Rights
- Criminal Justice
- Education
- Elections
- Energy
- Environment
- Government
- Healthcare
- Housing
- Labor
- Local Government
- Public Safety
- Taxes
- Transportation
- Utilities

### Requirements

- A bill may receive multiple topics.
- Taxonomy version must be stored.
- Manual correction must be possible.
- Topic tags should support search and future subscriptions.

---

# 13. Information Architecture

## 13.1 Primary public page types

MVP:

- `/`
- `/search`
- `/bills/{session}/{bill-slug}`
- `/topics/{topic}`
- `/legislators/{person-slug}`

Later:

- `/meetings/{meeting-id}`
- `/agencies/{agency-slug}`
- `/regulations/{regulation-id}`
- `/issues/{issue-slug}`
- `/municipalities/{municipality-slug}`

## 13.2 Bill page information hierarchy

The initial bill page should prioritize:

1. Bill identity and status
2. What changes
3. What happens next
4. Current version / recent change
5. Key provisions
6. Potentially affected groups
7. Timeline
8. Votes
9. Sponsors
10. Fiscal information
11. Source documents

Detailed procedural metadata should not dominate the top of the page.

---

# 14. User Experience Requirements

## 14.1 Mobile-first

The product should be designed for users arriving from:

- search engines,
- social media,
- messaging,
- local news,
- shared links.

A mobile user opening a bill should immediately be able to determine:

1. what it is,
2. what it changes,
3. where it stands,
4. what can happen next.

## 14.2 Progressive disclosure

Top-level content should remain concise.

Deeper layers should expose:

- full timeline,
- complete vote records,
- version comparison,
- fiscal documents,
- legal text,
- source passages.

## 14.3 Jargon assistance

Government terms such as:

- engrossed,
- tabled,
- reported out,
- substitute,
- fiscal note,
- enrolled,
- veto,
- concurrent resolution,

should have inline definitions where useful.

Definitions should describe Delaware procedure where state-specific meaning matters.

---

# 15. Data Source and Authority Model

## 15.1 Source hierarchy

The platform should prefer sources in this order:

1. **Official Delaware government primary records**
2. **Official government-derived structured data**
3. **Platform-computed structured transformations**
4. **Attributed third-party reporting or analysis**
5. **AI-generated interpretation**

Lower layers must never silently override higher layers.

## 15.2 Source identity

Each ingested source should retain:

- publisher,
- canonical URL,
- retrieved timestamp,
- content hash,
- document type,
- effective/publication date where available,
- source identifier,
- related civic entities.

## 15.3 Raw-source retention

Where legally and technically practical, preserve immutable raw or normalized snapshots sufficient to:

- reproduce transformations,
- investigate errors,
- compare versions,
- and audit generated content.

## 15.4 Coverage transparency

The platform must not imply complete coverage when a source is partial.

Examples:

- A public meeting calendar may contain only agencies/bodies participating in that system.
- A state open-data dataset may update monthly.
- A legislative page may omit machine-readable text for certain fiscal or appropriations documents.
- Municipal systems may have inconsistent coverage.

Coverage limitations should be documented at the source level.

---

# 16. Current Delaware Source Strategy

## 16.1 Delaware General Assembly

Current public bill pages expose useful fields including:

- bill/session identity,
- status,
- introduced date,
- sponsors,
- synopsis,
- effective date,
- text versions,
- fiscal-note/fee-impact state,
- amendments,
- committee reports/history,
- roll calls,
- action history,
- and, for enacted legislation, session-law information.

### Implementation note

Do **not** assume a documented public legislation API exists until engineering discovery confirms one.

Phase 1 integration may need to rely on:

- public HTML,
- linked HTML documents,
- PDFs where necessary,
- or undocumented endpoints only after legal/technical review.

The connector should isolate source-specific extraction from the normalized civic model.

## 16.2 Delaware Public Meeting Calendar

Delaware's Government Information Center documents a REST API that returns JSON for the statewide Public Meeting Calendar.

This is a strong candidate for Phase 2.

Important caveat:

The existence of a statewide calendar does not guarantee every Delaware local-government meeting is represented. Coverage should be measured empirically.

## 16.3 Delaware Register of Regulations

The Delaware Register publishes proposed and final regulations and exposes web-accessible records containing:

- agency,
- legal authority,
- proposed/final text,
- publication context,
- public-comment instructions,
- hearing details where applicable,
- final orders,
- and effective dates.

Phase 3 should confirm the stability and supported use of the apparent machine-readable/API-style endpoints before treating them as a contractual API.

## 16.4 Delaware Open Data / financial data

Delaware's Open Data portal exposes state datasets through machine-readable interfaces such as OData.

Relevant future datasets include:

- state expenditures/checkbook information,
- statewide central contract spend,
- procurement-related records.

These are Phase 4 inputs, not MVP dependencies.

---

# 17. Data Freshness and Staleness

Government data changes at different speeds.

The product should define freshness by source type rather than make one universal promise.

## MVP targets

### Active legislation during session
Target ingestion check: **at least hourly during configured active legislative windows**, subject to source behavior and rate limits.

### Inactive or historical legislation
Target ingestion check: **daily or less frequently** after terminal state.

### Public meetings — Phase 2
Target ingestion check: **hourly** for upcoming meetings and agendas.

### Regulations — Phase 3
Target ingestion check: **daily** unless source update behavior justifies a faster cadence.

### Financial data — Phase 4
Follow source publication cadence.

## User-facing freshness

Pages should expose:

> **Source last checked:** DATE / TIME

When data exceeds its expected freshness threshold:

> **This information may be stale. We have not successfully refreshed the source since DATE/TIME.**

---

# 18. State Model and Material Events

Engineering and product should define a normalized legislative state machine.

Illustrative states include:

- Introduced
- Assigned to committee
- Committee activity
- Reported/released from committee
- Eligible for floor consideration
- Passed originating chamber
- Received by second chamber
- Second-chamber committee
- Passed both chambers
- Awaiting governor action
- Signed
- Vetoed
- Veto overridden
- Failed/defeated
- Expired/end of session
- Unknown/other

The model must preserve the raw official status in addition to the normalized status.

## Material-event definition

Notifications and "recently changed" UI should eventually focus on material events such as:

- new bill version,
- amendment/substitute,
- committee release,
- scheduled hearing,
- chamber passage,
- governor action,
- fiscal-note publication,
- major deadline,
- effective-date change.

Minor metadata refreshes should not be treated as policy changes.

---

# 19. AI Product Requirements

AI is an interpretation layer, not a source of record.

## 19.1 Allowed uses

AI may:

- summarize legislation,
- explain legal language,
- compare identified source versions,
- classify topics,
- extract candidate implementation requirements,
- summarize agendas,
- identify named entities,
- generate embeddings for discovery,
- explain procedural statuses from structured context,
- extract candidate dates/deadlines,
- identify possible relationships for later verification.

## 19.2 Restricted uses

AI must not present as established fact:

- lawmakers' motivations,
- predicted votes,
- ideological classifications not sourced to a defined methodology,
- corruption allegations,
- causation unsupported by evidence,
- economic outcomes without evidence,
- beneficiaries or harmed groups without support,
- future events that are merely possible.

## 19.3 AI output contract

Every generated content object should internally record:

- generation type,
- model/version,
- prompt/template version,
- source IDs,
- source version IDs,
- generated timestamp,
- validation results,
- publication status.

## 19.4 Generation states

Suggested internal states:

- Generated
- Validated
- Published
- Superseded
- Flagged
- Withheld

## 19.5 Fallback behavior

If generation fails or confidence is insufficient:

- continue showing structured facts,
- link to the official source,
- omit the AI explanation,
- state that a plain-language explanation is not currently available.

The product must remain useful when AI is unavailable.

---

# 20. AI Quality and Validation

## 20.1 Deterministic fields

The following should not rely on free-form model generation when structured data is available:

- bill number,
- status,
- sponsor names,
- vote totals,
- vote records,
- dates,
- effective dates,
- money amounts,
- committee identity,
- document version,
- session,
- source URLs.

## 20.2 Numeric validation

Extracted numeric facts should be checked against source text before publication.

High-priority types:

- dollars,
- percentages,
- dates,
- thresholds,
- age limits,
- vote counts,
- effective dates,
- deadlines.

## 20.3 Version validation

Before publishing a bill explanation:

1. identify the current operative source document,
2. verify it is newer/controlling relative to prior versions,
3. associate generation with that source version,
4. mark previous generated explanations as superseded.

## 20.4 Contradiction detection

If sources disagree, the product should:

- preserve both source records,
- flag the conflict,
- avoid silently choosing an answer when the authoritative hierarchy does not resolve it.

## 20.5 Evaluation set

Before public launch, create a human-reviewed benchmark set covering:

- simple bills,
- long/complex bills,
- substitutes,
- multiple amendments,
- appropriations,
- fiscal notes,
- resolutions,
- bills changing definitions,
- bills with delayed effective dates,
- bills with no fiscal note,
- enacted and failed legislation.

Evaluation dimensions:

- factual accuracy,
- completeness,
- current-version correctness,
- neutrality,
- citation correctness,
- readability,
- procedural accuracy.

---

# 21. Citation Requirements

For generated substantive claims, citations should be claim-level or section-level rather than attaching a generic list of sources to the bottom of a page.

A citation should resolve to:

- source document,
- relevant location/section if available,
- source version,
- official publisher.

The user should be able to inspect the source without trusting the generated explanation.

---

# 22. Correction and Dispute Mechanism

Users should be able to report:

- inaccurate summary,
- stale status,
- incorrect source relationship,
- wrong topic,
- missing source,
- incorrect version,
- misleading interpretation.

Corrections should distinguish:

- source-data issue,
- ingestion issue,
- extraction issue,
- model-generation issue,
- editorial issue.

Internal records should retain:

- report timestamp,
- affected entity,
- correction category,
- resolution state,
- resolution note,
- resulting regeneration or data repair.

---

# 23. Accessibility

Target:

**WCAG 2.2 AA**

Requirements include:

- keyboard navigation,
- semantic HTML,
- readable typography,
- screen-reader support,
- sufficient contrast,
- accessible tables,
- accessible interactive timelines,
- visible focus states,
- descriptive link text,
- responsive layout.

Plain-language comprehension should be treated as part of accessibility.

---

# 24. Privacy

The MVP should minimize personal data collection.

## MVP recommendation

- Reading and searching should not require an account.
- Avoid collecting precise residential addresses in MVP.
- If analytics are used, collect only what is needed to improve the product.

## Future address-based personalization

If a future user provides an address to identify:

- districts,
- representatives,
- municipality,
- school district,
- local jurisdiction,

then product design must define:

- whether raw addresses are stored,
- whether geocoding can occur ephemerally,
- retention policy,
- deletion behavior,
- third-party geocoder data handling.

Preferred principle:

> Retain derived civic districts rather than precise address data whenever practical.

---

# 25. Security and Integrity

Because the product concerns public civic information, integrity is a product requirement.

At minimum:

- sanitize ingested HTML,
- validate external links,
- protect ingestion pipelines from malformed content,
- preserve source provenance,
- restrict internal editing privileges,
- maintain audit trails for manual overrides,
- separate user-submitted correction content from authoritative content,
- rate-limit abusive automated access where necessary.

Generated text must not be able to overwrite authoritative source fields.

---

# 26. SEO and Public Discovery

Most civic content should be publicly indexable.

Example routes:

- `/bills/153/HB-350`
- `/topics/housing`
- `/legislators/jane-smith`

SEO metadata should clearly identify:

- jurisdiction,
- session,
- bill number,
- current status,
- canonical URL.

Structured data may be added where relevant and valid.

The goal is to allow residents to discover civic information through ordinary search rather than requiring habitual use of a dedicated app.

---

# 27. Sharing

Every issue should be easy to share without stripping away context.

A shared preview should preserve:

- bill number,
- neutral short description,
- current status,
- last updated date,
- canonical product URL.

Future functionality may generate:

- social cards,
- newsletter embeds,
- short issue summaries,
- shareable timeline events.

Generated social language should remain factual and neutral by default.

---

# 28. Analytics and Instrumentation

The product should measure whether users understand and investigate issues—not merely whether pages receive traffic.

## Core events

Suggested events include:

- search_submitted
- search_result_opened
- bill_summary_viewed
- source_opened
- timeline_expanded
- version_comparison_opened
- vote_record_opened
- fiscal_note_opened
- what_happens_next_viewed
- participation_information_opened
- correction_submitted
- topic_opened
- return_visit

## Search-quality metrics

Track:

- zero-result rate,
- reformulation rate,
- result click-through,
- bill-number success rate,
- semantic search success from sampled review.

---

# 29. Success Metrics

## 29.1 Comprehension

Potential measures:

- percentage of bill-page visitors reaching **What changes**
- percentage viewing **What happens next**
- optional task-based user testing
- "Did this answer your question?" feedback
- source expansion rate

## 29.2 Discovery

- successful searches
- topic-to-bill exploration
- zero-result rate
- search reformulation rate
- related-item engagement

## 29.3 Trust

- official-source click-through
- user-reported error rate
- confirmed correction rate
- stale-data incidents
- citation resolution success
- user trust survey

## 29.4 Civic action — Phase 2+

- meeting-detail views
- public-comment link opens
- official contact link opens
- calendar-event additions
- participation subscriptions

## 29.5 Retention — Phase 2+

- returning users
- followed topics
- followed bills
- alert engagement

---

# 30. North Star Metric

A long-term North Star could be:

> **Monthly Informed Civic Actions**

An Informed Civic Action is a session in which a user consumes issue context and then performs a meaningful high-intent action such as:

- opening an official source,
- reviewing a vote,
- comparing versions,
- following an issue,
- viewing an upcoming meeting,
- checking representation,
- accessing public-comment information.

This metric requires careful definition to avoid treating any click as genuine civic understanding.

For MVP, the better primary metric may be:

> **Successful Legislative Understanding Sessions**

A session qualifies when a user finds a bill and consumes at least one explanatory component plus one verification or process component.

This should be validated through user research before becoming an executive KPI.

---

# 31. Observability and Operations

The platform should expose internal health for each source connector.

Track:

- last successful ingestion,
- last failed ingestion,
- source response changes,
- records discovered,
- records updated,
- parsing failures,
- schema/extractor anomalies,
- generation queue failures,
- stale entities,
- source-link failures.

High-severity alerts should include:

- active legislation not refreshed within freshness SLA,
- widespread source parser failure,
- broken canonical source URLs,
- incorrect current-version detection,
- vote data mismatch,
- generation publishing without provenance.

---

# 32. Launch Criteria

The MVP should not launch publicly until the following are true.

## Data

- Current General Assembly bills are ingested with agreed coverage.
- Core source fields have measured extraction accuracy.
- Version identity is reliable for supported bill types.
- Vote records are validated for supported roll calls.
- Source freshness monitoring is active.

## AI

- Benchmark evaluation meets agreed quality thresholds.
- Generated explanations cannot publish without source IDs.
- Current-version changes invalidate/supersede old summaries.
- Numeric and date validation gates are operational.
- Failure falls back to structured data rather than blocking the page.

## UX

- Search works for bill number and common policy queries.
- Bill pages are usable on mobile.
- Primary sources are one interaction away from the explanation.
- Accessibility review is complete for critical journeys.

## Operations

- Ingestion failures generate alerts.
- Corrections can be submitted and processed.
- Manual source/entity overrides are auditable.
- Product can show stale-data warnings.

---

# 33. Suggested MVP User Stories

## Search

**As a Delaware resident,** I want to search "hospital costs" so that I can discover legislation even when I do not know a bill number.

## Understanding

**As a citizen,** I want a plain-language explanation of the current bill so that I do not have to interpret legislative drafting myself.

## Verification

**As a skeptical user,** I want to open the exact government source supporting an explanation so that I can verify it.

## Procedure

**As a citizen,** I want to understand what can happen after the bill's current status so that I know whether the process is finished.

## Version change

**As a returning user,** I want to know that a substitute materially changed the bill so that I do not rely on an outdated summary.

## Voting

**As a citizen,** I want to see the official roll call so that I know how legislators voted.

## Fiscal impact

**As a citizen,** I want fiscal-note information clearly separated from general commentary so that I know which cost claims come from the state.

---

# 34. Phase 2 — Public Meetings and Civic Action

Integrate Delaware's Public Meeting Calendar.

Users should be able to discover:

- upcoming hearings,
- agency meetings,
- committee activity,
- workshops,
- and other relevant public meetings available in the source.

Meetings should be associated, where evidence supports the relationship, with:

- bills,
- agencies,
- regulations,
- topics,
- or issues.

## Meeting detail

Display:

- date,
- time,
- organization,
- location,
- remote participation details,
- agenda,
- agenda topics,
- public-comment instructions when present,
- supporting documents,
- minutes when available.

## Relationship confidence

A meeting-to-bill or meeting-to-topic relationship should distinguish:

- explicit source relationship,
- deterministic identifier match,
- high-confidence extracted relationship,
- editorially verified relationship.

Low-confidence semantic similarity should not silently create a public factual connection.

---

# 35. Phase 3 — Regulation Tracking

Create links between legislation and administrative regulation.

Conceptually:

**Legislation**  
↓ grants or changes authority

**Agency**  
↓ proposes

**Regulation**  
↓ receives

**Public comment / hearing**  
↓ becomes

**Final regulation**

## Regulation page should eventually answer

- What is the agency proposing?
- What existing regulation changes?
- What statutory authority is cited?
- When are comments due?
- Is there a hearing?
- What changed between proposal and final rule?
- When does the final rule take effect?
- Which legislation or statute is related?

Relationships must be evidence-based.

---

# 36. Phase 3+ — Post-Passage Implementation

For enacted legislation, identify implementation requirements.

Examples:

- agency must issue regulation,
- report due by date,
- program must launch,
- commission must be created,
- fee schedule must be established,
- funding must be appropriated,
- study must be conducted.

## Proposed implementation object

Each extracted obligation should contain:

- source law,
- responsible entity,
- required action,
- statutory deadline if any,
- source passage,
- confidence/review state,
- evidence of completion,
- current observed status.

### Critical wording rule

If no evidence of completion is found:

> **No completion evidence identified in monitored sources.**

Do not automatically claim:

> **Not completed.**

Absence of evidence is not always evidence of noncompliance.

---

# 37. Phase 4 — Policy, Money, and Influence Graph

Add:

- budget records,
- appropriations,
- contracts,
- expenditures,
- lobbying,
- campaign-finance records.

Potential relationships:

**BILL → AUTHORIZES → PROGRAM**

**APPROPRIATION → FUNDS → PROGRAM/AGENCY**

**AGENCY → AWARDS → CONTRACT**

**CONTRACT → PAID_TO → VENDOR**

**LOBBYIST → REGISTERED_FOR → ORGANIZATION**

**LOBBYING DISCLOSURE → REFERENCES → ISSUE/BILL**  
only when the public record explicitly supports that relationship.

The platform must avoid implying that donations, lobbying, sponsorship, or votes prove improper influence.

---

# 38. Phase 5 — Government Responsibility Router

Allow a user to describe a real-world issue.

Example:

> Who controls the road outside my neighborhood?

The platform attempts to determine:

1. issue category,
2. physical jurisdiction if relevant,
3. government level,
4. responsible body,
5. responsible agency/department,
6. elected representation,
7. relevant processes,
8. known meetings or participation channels.

Example output:

**Likely road owner:** Delaware Department of Transportation  
**Responsible organization:** DelDOT  
**Relevant district:** [if derived]  
**Reporting mechanism:** official government link  
**Related public process:** [if one exists]

The system must clearly distinguish "likely responsibility" from verified ownership when authoritative GIS or asset data is unavailable.

---

# 39. Civic Knowledge Graph

The long-term data model should support connected civic entities.

## Core entity types

- Bill
- Bill Version
- Amendment
- Vote
- Vote Record
- Legislator
- Person
- Office
- District
- Committee
- Meeting
- Agenda Item
- Agency
- Regulation
- Statute
- Budget Item
- Fiscal Note
- Contract
- Vendor
- Expenditure
- Organization
- Lobbyist
- Campaign
- Municipality
- Topic
- Source Document
- Implementation Obligation

## Example relationships

**LEGISLATOR**  
`SPONSORS → BILL`

**BILL**  
`REFERRED_TO → COMMITTEE`

**AMENDMENT**  
`MODIFIES → BILL_VERSION`

**BILL_VERSION**  
`SUPERSEDES → BILL_VERSION`

**BILL**  
`RESULTS_IN → SESSION_LAW`

**STATUTE**  
`AUTHORIZES → AGENCY`

**REGULATION**  
`CITES_AUTHORITY → STATUTE`

**AGENCY**  
`RECEIVES → APPROPRIATION`

**AGENCY**  
`AWARDS → CONTRACT`

**CONTRACT**  
`PAID_TO → VENDOR`

The graph does not need to be directly visible to ordinary users.

It powers:

- search,
- provenance,
- recommendations,
- timelines,
- issue pages,
- implementation tracking,
- and future investigative tools.

---

# 40. Technical Product Principles

This PRD does not prescribe a final architecture, but implementation should preserve the following product properties.

## 40.1 Structured ingestion

Normalize civic entities instead of building only a document-search/RAG system.

## 40.2 Source-specific connectors

Extraction logic for Delaware government sites should be isolated from the canonical domain model.

## 40.3 Immutable source/version identity

Preserve enough source history to reproduce and audit changes.

## 40.4 Event-driven enrichment

When a source changes:

1. ingest the new record,
2. identify affected entities,
3. compare against prior state,
4. invalidate stale derived content,
5. regenerate affected explanations,
6. eventually notify subscribed users if the change is material.

## 40.5 AI as enrichment

Core structured facts should remain available when AI processing fails.

## 40.6 Search plus structured relationships

Use search for discovery and structured entity relationships for authoritative connections.

Vector similarity alone must not establish factual civic relationships.

---

# 41. Dependencies

MVP depends on:

- reliable access to Delaware General Assembly public records,
- a robust method for identifying source/version changes,
- extraction of HTML and selected PDFs where required,
- search indexing,
- source-provenance storage,
- an AI generation service,
- validation/evaluation tooling,
- monitoring.

Later phases depend on:

- Public Meeting Calendar API integration,
- reliable Register of Regulations ingestion,
- entity resolution across agencies/statutes/bills,
- geographic/district data,
- state open-data financial sources.

---

# 42. Key Assumptions to Validate

1. Delaware legislative source pages remain publicly accessible and can be monitored at an acceptable cadence.
2. The product can reliably identify the current operative text for supported bill types.
3. Source terms and technical behavior permit the planned ingestion pattern.
4. Plain-language summaries materially improve comprehension versus the official synopsis alone.
5. Users value "What happens next?" enough for it to drive differentiation.
6. Topic search is a more common entry path than exact bill-number search for general citizens.
7. Primary-source citations increase trust.
8. Citizens care about implementation after passage when the lifecycle is presented clearly.
9. Meeting discovery becomes substantially more useful when connected to an issue a user already cares about.
10. Search and shared issue pages will be stronger acquisition channels than habitual direct homepage traffic.

---

# 43. Key Risks and Mitigations

## Risk — AI hallucination

**Mitigation:**
- source-backed generation,
- deterministic fact fields,
- numeric validation,
- version validation,
- fallback to structured data.

## Risk — Political-bias perception

**Mitigation:**
- standardized templates,
- transparent methodology,
- primary-source citations,
- symmetric presentation,
- attribution,
- public corrections.

## Risk — Source changes break ingestion

**Mitigation:**
- connector isolation,
- parser monitoring,
- raw-source retention,
- source-change alerts,
- automated test fixtures.

## Risk — Wrong bill version summarized

**Mitigation:**
- version-first processing,
- source version IDs,
- invalidation on change,
- regression test set.

## Risk — False entity relationships

**Mitigation:**
- relationship provenance,
- confidence states,
- rules before semantic inference,
- manual review for ambiguous high-impact links.

## Risk — Information overload

**Mitigation:**
- progressive disclosure,
- mobile-first hierarchy,
- citizen-oriented language,
- preserve source detail behind expandable views.

## Risk — Low repeat engagement

**Mitigation:**
- initially optimize for search/share acquisition,
- add topic following and material-change alerts in Phase 2,
- avoid requiring accounts for core use.

## Risk — Incomplete public datasets

**Mitigation:**
- source coverage metrics,
- explicit incomplete-coverage language,
- never equate "not in our data" with "does not exist."

---

# 44. Open Product Decisions

These should be resolved through discovery and prototyping rather than assumed.

## Search scope

Should MVP include historical sessions or current General Assembly only?

**Recommended default:** Current session first, with historical retrieval only if ingestion cost is low and the UX clearly labels it.

## Accounts

Should users be able to create accounts in MVP?

**Recommended default:** No. Delay accounts until following/notifications create real user value.

## AI chat

Should the product expose a free-form chat interface?

**Recommended default:** Not initially. Establish trustworthy structured pages and retrieval first.

## Editorial review

Which generated explanations require human review?

Candidates:

- highly complex appropriations,
- major constitutional changes,
- election administration,
- ambiguous version chains,
- content flagged by validation.

## News integration

Should local journalism be attached to issue records?

Potentially valuable, but it should be presented as **reporting/context**, not mixed with primary government evidence.

## User discussion

Should citizen comments/discussion exist?

**Recommended default:** No in early releases. Moderation and trust costs are high and do not validate the core product thesis.

## Position statements

Should elected officials or organizations be able to attach verified positions to legislation?

Potentially useful later, but identity verification, moderation, and equal-access policy are prerequisites.

---

# 45. Product Hypotheses and Experiments

## H1 — "What happens next?" is more valuable than raw legislative history

**Experiment:** Compare engagement and comprehension for a status-only page versus a status + procedural-next-step page.

## H2 — Users search by issue more often than bill number

**Experiment:** Instrument search categories and recruit users with recent Delaware news prompts.

## H3 — Source transparency increases trust

**Experiment:** Compare trust ratings for summaries with persistent inline source affordances versus a generic sources section.

## H4 — Version-change explanations create repeat value

**Experiment:** Test whether returning users can correctly identify what changed after seeing a structured version-diff summary.

## H5 — Post-passage implementation is a meaningful unmet need

**Experiment:** Build a manual prototype for 10 enacted Delaware laws with implementation obligations and test with citizens, journalists, and civic organizations.

## H6 — Issue-linked meeting alerts drive engagement

**Experiment:** In Phase 2, compare generic meeting discovery with alerts linked to a bill/topic the user already viewed or followed.

---

# 46. Suggested Delivery Epics

## Epic 1 — Source ingestion foundation

- General Assembly connector
- raw source capture
- source IDs/hashes
- normalized bill identity
- refresh scheduling
- connector monitoring

## Epic 2 — Legislative domain model

- bills
- versions
- actions
- sponsors
- committees
- votes
- fiscal notes
- source relationships

## Epic 3 — Search and discovery

- exact bill lookup
- keyword search
- semantic retrieval
- topic taxonomy
- ranking
- result cards

## Epic 4 — Bill detail experience

- header
- status
- key provisions
- source documents
- timeline
- sponsors
- votes
- fiscal section

## Epic 5 — Version intelligence

- version identity
- source diff
- amendment/substitute mapping
- "what changed" experience
- supersession behavior

## Epic 6 — AI explanation pipeline

- generation templates
- source grounding
- provenance
- validation
- regeneration/invalidation
- fallback behavior

## Epic 7 — Procedural intelligence

- normalized state machine
- "What happens next?"
- state-specific explanations
- terminal states
- test fixtures

## Epic 8 — Trust and quality

- citations
- correction workflow
- quality benchmark
- stale-data UI
- audit metadata

## Epic 9 — Production readiness

- accessibility
- SEO
- analytics
- observability
- security hardening
- launch gates

---

# 47. MVP Release Definition

The MVP is successful when a user can:

1. search current Delaware legislation,
2. find a relevant bill by number or issue,
3. understand the current bill in plain language,
4. distinguish current text from superseded text,
5. see current status,
6. understand major legislative history,
7. identify meaningful amendments/substitutes,
8. inspect official votes,
9. inspect fiscal-note information where available,
10. understand what procedural steps are possible next,
11. verify substantive explanations against authoritative sources.

The MVP should prove that citizens can move from:

> **I heard something is happening in Delaware government**

to:

> **I understand what the current proposal changes, where it is in the process, and how to verify it**

in a few minutes.

---

# 48. Post-MVP Strategic Differentiation

The product should avoid positioning itself as:

> **An easier Delaware bill tracker.**

The stronger positioning is:

> **A system for understanding what Delaware government is doing, what changes, what happens next, and how citizens can participate.**

The long-term competitive moat is the structured civic graph connecting:

**legislation + people + meetings + regulations + agencies + participation + implementation + public money**

while retaining provenance back to public records.

---

# 49. Delaware Source Verification Appendix

The following official public sources were re-checked while preparing version 0.2 on October 9, 2026.

## Delaware General Assembly

Example current bill pages expose fields including status, sponsors, fiscal-note/fee-impact state, effective date, bill text, amendments, committee reports, roll calls, and action history.

- https://legis.delaware.gov/
- Example bill detail: https://legis.delaware.gov/BillDetail?LegislationId=143511

**Product implication:** Phase 1 has strong public source material, but engineering discovery must determine the most reliable and supportable ingestion interface. This PRD does not assume an official public legislation API.

## Delaware Public Meeting Calendar

The Government Information Center documents a REST API using HTTPS GET methods that return JSON data.

- https://gic.delaware.gov/state-public-meeting-calendar/

**Product implication:** Phase 2 can likely use a documented machine-readable source rather than relying exclusively on scraping. Coverage completeness still needs measurement.

## Delaware Register of Regulations

The Register publishes proposed and final regulations, legal authority, comment/hearing information, and effective-date/final-order material.

- https://regulations.delaware.gov/

**Product implication:** This is a strong Phase 3 source for connecting statutes, agencies, proposed rules, public comment, and final regulations. Engineering should validate any API-style endpoint before treating it as a stable contractual API.

## Delaware Open Data

The state's Open Data portal publishes machine-readable government datasets, including expenditure and contract-spend data.

- https://data.delaware.gov/
- Statewide Central Contract Spend: https://data.delaware.gov/Government-and-Finance/Statewide-Central-Contract-Spend/sifm-293u

**Product implication:** Phase 4 can build on public structured financial data, but individual dataset refresh cadences and schemas must be modeled explicitly.

---

# 50. Final Recommendation

The product should begin with a deliberately narrow wedge:

> **Delaware legislative understanding with reliable version awareness, source-backed plain language, and deterministic procedural context.**

Do not delay the MVP by trying to solve meetings, regulations, spending, lobbying, personalization, or municipal government at once.

At the same time, build the underlying domain model so those layers can connect later.

The most important architectural/product decision is therefore:

> **Treat bills as connected, versioned civic entities—not as documents to summarize.**

If that foundation is correct, the platform can expand naturally from:

**Bill understanding**  
→ **Civic participation**  
→ **Regulatory implementation**  
→ **Government accountability**  
→ **Local-government navigation**

without needing to rebuild the product around each new dataset.
