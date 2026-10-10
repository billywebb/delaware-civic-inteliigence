# Delaware Legislative Source Discovery Plan

## Context

The request is to read `delaware_civic_intelligence_prd_v0.2.md` and discuss a delivery plan. The complete 2,585-line PRD has been read; the project root listing contains only that document and no application implementation. The intended product end state is the complete Phase 1 legislative intelligence MVP defined by FR-1 through FR-14 and the public-launch requirements, not the later meetings, regulations, financial, or municipal phases.

The selected next deliverable is a read-only source-and-version feasibility investigation, not application implementation. Every AI explanation in the eventual public product, including regenerated explanations, requires human approval; automated validation does not replace that approval.

## Findings

- The PRD requires current-version correctness, immutable source identity, claim/section citations, deterministic factual fields, procedural rather than political predictions, and structured-data fallback when AI is unavailable.
- The PRD explicitly does not confirm a supported public legislation API. Source access, permitted ingestion, discovery enumeration, and operative-text resolution remain unverified — confirm first.
- Reading https://legis.delaware.gov/BillDetail?LegislationId=143511 returned Senate Bill 335 of the 153rd General Assembly, status `Signed 6/30/26`, sponsor links, a synopsis, fiscal-note status `Not Required`, session law `85:324`, and a linked PDF at `/json/BillDetail/GetPdfDocument?fileAttachmentId=655594`.
- That official page already has `What typically happens next?` and the explanation `Becomes effective upon date of signature of the Governor or upon date specified`. Procedural wording alone is therefore not a demonstrated differentiation; combine it with version-aware explanations and inspectable evidence.
- Browser inspection confirmed that committee, roll-call, and action rows load dynamically. SB 335 has two committee reports, two chamber roll calls, and seven action-history rows; only its amendment table explicitly says `No Records Available`. The House roll call is 36 Yes, 3 No, 1 Not Voting, 1 Absent; the Senate roll call is 21 Yes, 0 No, 0 Not Voting, 0 Absent.
- Observed page-generated read requests use POST routes under `/json/BillDetail/`: `GetRelatedAmendmentsByLegislationId`, `GetCommitteeReportsByLegislationId`, `GetVotingReportsByLegislationId`, and `GetRecentReportsByLegislationId`, each with `?legislationId=143511`. These observations establish browser behavior, not a supported API contract or permission for direct automation.
- The linked SB 335 PDF is readable through document extraction. Its first page identifies a 240-page appropriations bill; the opening section contains deletion/insertion markup changing fiscal-year dates from 2026 to 2027. Text extraction needs review for drafting markup and table-column fidelity before it can support a summary.
- The rendered page links `View All Legislation` to https://legis.delaware.gov/AllLegislation and `RSS Feeds` to https://legis.delaware.gov/RssFeed.
- The rendered All Legislation page defaults to GA 153 and displays 20 rows per page, with `1 - 20 of 1962 items` observed during planning. Its filters include Bill, Resolution, Concurrent Resolution, Joint Resolution, Amendment, and Substitute. The count is all legislation records under the displayed filters, not a validated count of bills. Its page-generated data request is POST `/json/AllLegislation/GetAllLegislation`.
- The first listing page links HB 471 with HA 1, HA 2, HA 3 at https://legis.delaware.gov/BillDetail?LegislationId=143499 and HB 470 with HA 3 at https://legis.delaware.gov/BillDetail?LegislationId=143449. These are discovery candidates; their operative text has not yet been resolved.
- The official SB 335 House roll-call PDF at https://legis.delaware.gov/json/RollCallController/GenerateRollCallPdf?rollCallId=58788&chamberId=2 is readable and lists individual votes, totals `36 YES 3 NO 1 NOT VOTING 1 ABSENT 0 VACANT`, Session 2, and timestamp `06/24/2026 08:13 PM`. Discover the source's vote-code legend before assigning category semantics to abbreviations.
- HB 471's inspected detail page exposes both original text and Final/Engrossed text (`engrossmentId=38221`), with Signed 7/23/26 and chapter 85:411. Resolve incorporated amendments from rendered actions before treating that artifact as controlling.
- HS 1 for HB 320 at https://legis.delaware.gov/BillDetail?LegislationId=143542 explicitly links its parent HB 320, original text, and final engrossment (`engrossmentId=38251`). It is a constitutional-amendment first leg: its page says the 154th General Assembly must pass it, despite showing Passed 6/30/26 and Volume:Chapter 85:326. A chapter value alone cannot establish ordinary enactment.
- SA 1 to HB 75 at https://legis.delaware.gov/BillDetail/143671 has status `Stricken 7/1/26`; it is a concrete amendment record to investigate without incorporating it into current bill text.
- HB 500 at https://legis.delaware.gov/BillDetail/143658 is `Signed 7/6/26 (7/6/2026 Line-Item Veto - See Governor's Advisory #46)`. https://governor.delaware.gov/legislative-advisories/legislative-advisories-46/ confirms a line-item veto striking `Legislative Hall Addition $35,000,000`. Signed does not imply every original appropriation survived.
- The rendered official glossary states that defeated legislation can be restored within three legislative days; defines engrossed legislation as incorporating approved amendments; and states that constitutional amendments require two successive General Assemblies, without Governor signature/veto. Preserve these exceptions rather than directly copying the PRD's illustrative terminal-state list.
- The rendered https://legis.delaware.gov/RssFeed page publicly lists eight feeds: Introduced, Committee, Out of Committee, In Lieu, Stricken, House Passed, Senate Passed, and Governor Signed legislation. It explicitly warns that feed links change with each General Assembly. Feed coverage and reliability still need measurement; documentation does not establish a full legislation API or bulk-reuse permission.
- https://legis.delaware.gov/Footer/Copyright displays `© 2015 Delaware General Assembly. All Rights Reserved.` and a website-question contact `LISTeam@delaware.gov`. The inspected copyright and disclaimer pages do not specify automation rates or a reuse license; those questions remain unresolved. Do not infer prohibition or permission from the copyright notice alone.
- No technology choice, source-access permission, source-rate allowance, complete extraction accuracy, or human-review capacity has been established.

## Approach

Execute this milestone as a read-only investigation. Do not install dependencies, create an application, start a crawler, generate explanations, or alter the PRD. The deliverable is `local://legislative-source-findings.md`, a session-local evidence report; create it at the start and record findings incrementally. No equivalent investigation report or source connector exists in the inspected project.

Use these report sections: `Access and interface evidence`, `Enumeration`, `Representative records`, `Version resolution`, `Votes and fiscal records`, `Procedural sources`, and `Feasibility verdict`. Each factual finding needs its exact official URL, retrieval time, observed evidence, and any unresolved limitation.

### 1. Establish the access boundary

Read https://legis.delaware.gov/Footer/Copyright and https://legis.delaware.gov/Footer/Disclaimer, the feed-help linked from the RSS index, and developer/API documentation if discovered. Inspect https://legis.delaware.gov/robots.txt as access evidence, not as a license. Record separately: documented supported interface, observed public interface, explicit permitted/prohibited use, and unknown authorization/rate limits. Absence of a restriction or documentation proves neither permission nor support. Identify `LISTeam@delaware.gov` as the observed website-contact route for unresolved supported-use questions; do not send mail during this milestone.

Prefer static `read` for ordinary documents and the managed browser for JavaScript-rendered tables. Browser-generated POST requests that populate views are read operations; inspect their method, URL, and payload without replaying or modifying them. Do not submit subscriptions, contact forms, corrections, or any other write operation on government sites. If a CAPTCHA, denial, or explicit prohibition appears, do not bypass it; retain the failed URL/status and continue with permitted documents.

This step and procedural-source reading in step 4 are independent and may run concurrently. Record an unresolved authorization requirement as a prerequisite to production automation; it does not prevent completing the read-only discovery report.

### 2. Verify enumeration and assemble representative records

Open https://legis.delaware.gov/AllLegislation in the managed browser. Wait for actual legislation links, not just the initial empty grid. Record the currently selected General Assembly, checked type filters, displayed total, page size, ordering, canonical detail URLs, and numeric `LegislationId` query values. Navigate the next page through the visible pager and verify that its identifiers differ from page one. Toggle the visible Bill, Amendment, Substitute, and resolution-type filters individually, restoring the initial filters after each observation; record how totals and record identity change. Do not report an all-types count as the bill count.

Read https://legis.delaware.gov/RssFeed and its help links. Inspect each of the eight actual linked URLs under `https://legis.delaware.gov/RSSFeeds/`: `IntroducedLegislation`, `CommitteeLegislation`, `OutofCommitteeLegislation`, `InLieuLegislation`, `StrickenLegislation`, `HousePassedLegislation`, `SenatePassedLegislation`, and `GovernorSignedLegislation`. Follow observed redirects rather than assume another endpoint spelling. For each readable feed record HTTP outcome, final URL, content type, item count, source General Assembly identifiers, item links, and minimum/maximum item dates. Distinguish feed build/item timestamps from a bill's latest material action and successful source-check time. On failure, preserve the outcome, try one ordinary longer-timeout read, then mark the feed unavailable rather than replay internal requests or add a crawler. Compare feed identifiers to the sample and listing scopes; missing feed entries do not prove missing legislation. Record the documented General-Assembly link-change caveat. Do not claim complete ingestion or launch coverage from feeds or two listing pages.

Start the sample with SB 335 (`LegislationId=143511`) for appropriations/enactment and HB 471 (`LegislationId=143499`) for an original/final document pair. Inspect HB 470 (`LegislationId=143449`) as an additional amendment candidate. Discover further records through official listing filters and search. Select the first record in displayed ordering satisfying each missing case, accepting one record for multiple cases: simple bill; adopted amendment; filed but unadopted/rejected amendment; substitute; official fiscal note; simple/concurrent/joint resolution; delayed effective date; vetoed bill; failed bill. Also inspect an end-of-General-Assembly record if the source exposes one; do not infer expiration from today's date.

Add fixed edge-case seeds: HS 1 for HB 320 at https://legis.delaware.gov/BillDetail?LegislationId=143542 and its linked parent for substitute/constitutional-first-leg behavior; SA 1 to HB 75 at https://legis.delaware.gov/BillDetail/143671 for a stricken amendment; HB 500 at https://legis.delaware.gov/BillDetail/143658 plus Governor Advisory #46 at https://governor.delaware.gov/legislative-advisories/legislative-advisories-46/ for signed-with-line-item-veto behavior. Investigate these in addition to, not instead of, ordinary bills and missing sample classes.

For each case, record bill identity, General Assembly and annual session when separately exposed, raw status, introduction/latest-action dates, sponsors, committees, amendments/substitute relations, all text links, source document identifiers/types, fiscal state, vote links, and action history. Mark an unavailable field `not exposed by inspected source`; retain literal values such as `Fiscal bill` rather than converting them into dates. When a case cannot be located through listing filters and official search, record the filters/queries tried and mark that case `unverified — unsupported pending additional source evidence`; never invent a fixture or silently omit the case.

### 3. Resolve document chains and extraction limits

For every sampled original/amended/substitute/enacted record, open all exposed original/final text documents and linked amendment/substitute detail pages. Establish whether each amendment is filed, adopted, rejected, or unknown from its official action/status. Compare parent/source identifiers across the detail pages rather than deriving relationships from semantic similarity or bill-number proximity.

For HB 471, inspect the original HTML linked with `GenerateHtmlDocument?legislationId=143499&legislationTypeId=1&docTypeId=2&legislationName=HB471` and final HTML linked with `GenerateHtmlDocumentEngrossment?engrossmentId=38221&docTypeId=6`, under https://legis.delaware.gov/json/BillDetail/. Read the supporting actions and amendments before identifying the final document as controlling. Record at least one actual changed passage and the source amendment responsible, or explicitly record that attribution could not be established.

Write a source-evidence table for each version chain: document URL/identifier, official document label, related amendment/substitute, adoption evidence, operative-text conclusion, and reason. Use only three conclusions: `resolved`, `ambiguous`, or `not available`. A newer file or a filed amendment is never sufficient evidence of current operative text. Where a final document is unavailable, determine whether the exposed original plus adopted amendments can be reconstructed deterministically from complete instructions. If not, mark the chain ambiguous and prescribe withholding the eventual current-version explanation; do not synthesize missing text during this investigation.

For enacted legislation, follow actual official links to Laws of Delaware/session-law text and Governor advisories; do not guess a session-law identifier from a bill identifier. Compare the displayed legislative text to enacted authority, particularly HB 500's vetoed appropriation. If enacted text cannot be retrieved or a line-item veto cannot be reconciled, mark enacted-text resolution ambiguous rather than summarize the unmodified original as law. On HS 1 for HB 320, retain the first-leg proposal state even though a chapter value exists.

Inspect the SB 335 PDF at https://legis.delaware.gov/json/BillDetail/GetPdfDocument?fileAttachmentId=655594. Review the opening year-change markup and one budget-table row against the original document view. Record whether extraction preserves additions/deletions, section/line/page anchors, amounts, units, and table-column alignment. For the sampled fiscal note, compare at least one amount and fiscal year to the document view. A readable string alone does not establish safe extraction.

### 4. Verify vote and procedural evidence

Read the SB 335 House roll-call PDF at https://legis.delaware.gov/json/RollCallController/GenerateRollCallPdf?rollCallId=58788&chamberId=2 and the corresponding rendered bill rows. Count individual vote categories, compare them to both the PDF totals and the rendered totals, and retain every official category, including `Vacant` when present. Confirm abbreviation meanings from an official legend or the bill's roll-call detail view; if unresolved, preserve raw codes and report the missing mapping rather than assume their semantics.

For a second sampled roll call, repeat reconciliation to check that one favorable example is not the entire vote feasibility proof. Record mismatches as conflicts; never silently choose between inconsistent official records. Distinguish `Not Required`, missing/unavailable, and a fiscal note with actual estimates; none permits an unsourced conclusion of zero cost.

Read the official glossary and both chamber rules linked from the bill page: https://legis.delaware.gov/Resources/GlossaryOfTerms, https://legis.delaware.gov/Chambers/House/house-rules, and https://legis.delaware.gov/Chambers/Senate/senate-rules. Follow their actual linked rule documents. Extract citation-backed definitions and procedural possibilities only for observed sample states, separately identifying bills, resolution types, and constitutional-amendment legs. Preserve the official site's existing next-step wording as an attributed source, not as a rule comprehensive enough to cover all states. Do not label defeated legislation irreversibly terminal, disregard the possibility of veto override, send constitutional amendments to the Governor, or infer expiration from a General Assembly year label. Unsupported procedural states remain unknown.

### 5. Deliver the feasibility verdict

In `Feasibility verdict`, answer separately whether observed public records support stable identity/enumeration, useful structured bill pages, current operative-text identification, source-linked comparisons, vote reconciliation, fiscal-document exposure, and cited procedural context. Give each capability `demonstrated`, `partial`, or `not demonstrated`, with evidence links and its exact missing prerequisite.

Specify the recommended ingestion surface using this fixed precedence: officially documented permitted interface if verified; otherwise observed public HTML/documents with rendered read views, explicitly contingent on automation permission and endpoint-support review. Do not recommend direct production use of undocumented JSON routes solely because they were observed in the browser. Specify which observed document classes can safely support explanations and which must be withheld pending resolution.

Close with the complete-MVP delivery sequence: trusted structured bill-page vertical slice; version-aware cited explanations and comparisons; FR-1 discovery/FR-14 topics and legislator pages; public-launch qualification against the PRD. Carry forward mandatory human approval tied to each source version, with new operative text invalidating both the old current explanation and its approval. This milestone does not choose or implement an application stack; the report supplies evidence for the subsequent implementation plan.

## Verification

Prerequisites: network access to official Delaware sites, `read`, and the managed `browser` helpers documented at `xd://eval/browser`. Working directory is the project root; no environment variables, dependency installation, application server, or test suite is needed. Use session-local artifacts only.

Run the actual source views. A minimal browser smoke command in JavaScript Eval is:

```javascript
const tab = await browser.open({
  name: "delaware-source-smoke",
  url: "https://legis.delaware.gov/BillDetail?LegislationId=143511"
});
await tab.waitForSelector("a[href*='GenerateRollCallPdf']", {timeout: 20000});
display(await tab.text("body"));
display((await tab.requests())
  .filter(r => ["xhr", "fetch"].includes(r.resourceType)
    && r.url.startsWith("https://legis.delaware.gov/"))
  .map(({method, url, status}) => ({method, url, status})));
await tab.screenshot({fullPage: true});
await tab.close();
```

Expected planning baseline: SB 335, GA 153, Signed 6/30/26; two committee reports; House totals 36/3/1/1 for Yes/No/Not Voting/Absent; Senate totals 21/0/0/0; seven action rows. If official records have legitimately changed, record the new evidence and reconcile against it instead of forcing the earlier baseline.

Required discovery proofs:

1. Show that the SB 335 static response omits populated committee/vote/action rows while its actual rendered view exposes them. Explicit `No Records Available` in the amendment table must be distinguished from unloaded or failed tables.
2. Show two distinct listing pages with their selected General Assembly, total, and identifiers; demonstrate that type filters alter record scope. Record current all-types versus bill-only totals without claiming full ingestion.
3. For HB 471, show the original and final documents, one specific textual change, and supporting amendment/actions, or give the exact unresolved attribution/version prerequisite. A chain marked resolved must have official evidence, not recency alone.
4. Reconcile SB 335's individual House votes to 36 Yes, 3 No, 1 Not Voting, 1 Absent, 0 Vacant using confirmed source category meanings; repeat for a second roll call. Any discrepancy remains visible in the report.
5. Verify the SB 335 year-change markup and one financial table row, plus one fiscal-note amount/year, against source views. Extraction problems produce a documented withholding constraint, not a guessed amount.
6. Every required representative case has an actual inspected record with evidence or a documented unsuccessful search and explicit unsupported status. Access permission, endpoint support, and hourly polling allowance are not marked verified without explicit evidence.
7. HS 1 for HB 320 remains a constitutional first-leg proposal despite its chapter field; the SA 1 to HB 75 chain does not absorb a stricken amendment; HB 500's signed status preserves its $35,000,000 line-item-veto qualification. Each conclusion cites official evidence rather than a generic terminal-state mapping.
8. Inventory all eight documented feeds with readable contents or recorded access failures, distinguish source date fields, and document the General-Assembly link-change warning. The observed HTML/POST read surface is not mislabeled as a documented supported legislation API.

The milestone is complete when the evidence report contains all prescribed sections and checks, with a capability-by-capability verdict and actionable missing prerequisites. It does not require inventing answers to unavailable source or legal facts. No application behavior, AI accuracy, production coverage, or launch readiness may be claimed from this discovery.

## Assumptions & contingencies

- User-selected next deliverable: discovery-first source-and-version investigation. Full Phase 1 remains the product destination; this plan authorizes no application implementation.
- User-selected initial publication policy: human approval of every explanation and regenerated version before public publication. Reviewer identity/capacity is not established; record it as an operational prerequisite, not a reason to weaken the policy.
- Recommended initial product boundary from the PRD: current General Assembly, without public accounts, chat, user discussion, historical-session backfill, or later-phase integrations. Historical sources may be read only to investigate a missing terminal/version case, clearly labeled as historical evidence.
- If a source URL or DOM changes, navigate from the official legislature entry point and use the newly observed public link/label; record the replacement and do not guess route parameters. If access remains unavailable after an ordinary static read and one ordinary browser navigation, preserve the error, continue reachable cases, and mark the capability partial/not demonstrated.
- If an important version, vote, fiscal, or procedural case lacks evidence, prescribe structured facts plus source links for that class and withhold unsupported derived explanations in the subsequent build. Missing source evidence must stay a reported prerequisite; no synthetic fixtures, unofficial substitute evidence, or access bypasses.

