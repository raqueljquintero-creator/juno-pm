# AI PRD · Juno

> Module 3 · Harness / AI PRD. The AI product requirements doc specifying all six harness surfaces, built with the **M3 · AI PRD Builder** (archetype and starting settings from the **M3 · Harness Architecture Decider**). Paste the tool's markdown over this file.

## Problem & user

_Rocketship ABC Product Managers receive information about product issues, enhancements and ideas on a daily basis and from different sources, and its difficult to keep track of each of them, the sources, frequency, related Jira tickets, among others. Juno is an insights-finding Product Assistant supporting RocketShip ABC Product Managers. It reviews evidence from customer, sales, and internal sources to identify patterns in issues, enhancements, and requests for new functionality; assesses their potential impact and risks for users, stakeholders, and RocketShip, and helps PMs decide what needs attention. The Product Managers remain responsible for priorities, decisions, and next steps._

_____

## The harness

| Surface | Specification |
|---|---|
| 01 Context | _what Juno gets to see_ |
| 02 Tools | _the verb list_ |
| 03 Loop | _turn ceiling and escalation_ |
| 04 Memory | _what persists, at what scope_ |
| 05 Permissions | _read … · draft … · write … · send …_ |
| 06 Verification | _the check before output ships_ |

## 01 Context · Data Requirements

### Required sources

Juno reviews these sources each day:

- The approved RocketShip Slack channels:
  - **“ABC PMs Only”**: where stakeholders and PMs discuss users’ issues, product enhancements, and ideas.
  - **“Rocketship Prod issues and highlights”**: where Rocketship technology teams discuss ABC product issues in production or at lower environments.
  - **“ABC Prod today”**: where the ABC delivery team and PMs discuss ABC production issues.
  - **“Juno’s daily review”**: where Juno posts its daily review. Juno may read its previous posts to check what was communicated and which review period was covered.
- The **“ABC Jira dashboard.”**
- The **“ABC Product Roadmap.”**
- **“Juno’s ABC Review Queue”**: where Juno drafts updates on issues, product enhancements, and ideas, which includes the PM comments and decision statuses.
- **“Sales pipeline snapshot”**: Juno reads **new or changed records from the approved CRM pipeline view** that includes customer needs, blockers, and sales commitments.
- **“Product Strategy One-Pager”**: which gives context about the vision of the Rocketship ABC product.
- Juno loads the approved Juno M1 Skill File as standing instructions.

**Complementary info on the tasks:**

- On the first run, Juno reads information created or updated during the previous 10 days. Later, it reads changes since the last successful review. It also compares new signals with earlier findings at “Juno’s ABC Review Queue” and existing Jira work.

### Deliberate exclusions

- The **“Engineering capacity Note”** is not relevant for Juno’s review since capacity limitations and their connection with priorities are handled by the product managers. **Excluding the Engineering Capacity Note should not prevent Juno from reporting technical risks found in approved sources.**
- Access to emails since not all the information included there will be relevant for Juno. The PMs will bring it to the allowed channels if applicable.
- Access to other Rocketship Slack channels, documents, and information not provided to Juno. Relevant information for Juno’s purpose is already included in the list of approved channels mentioned in the “Required sources” section.

### SLA of truth (how current the information must be)

- Start the daily review at **6:00 p.m. Mountain Time** and include information created or updated through that cutoff. Include later changes in the next review. On the first run, cover the previous ten days. For each source, recover updates missed since its last successful review. Show the version or last-updated date of reference documents when available; flag unknown freshness.

## 02 Tools · System Capabilities

### The verb list

1. **Read:** Search and read the approved sources listed in Context, including previous Juno posts, existing Jira work, and PM comments and decisions in Notion.
2. **Draft:** Prepare findings, evidence summaries, frequency updates, risks, clarification questions, and proposed new or updated Jira content.
3. **Save:** Create queue entries and update permitted fields in **“Juno’s ABC Review Queue,”** following the status and ownership rules in Permissions.
4. **Post:** Publish the daily summary and links to relevant queue entries in **“Juno’s daily review.”**

### Deliberate omissions

- No tools to create, edit, or delete Jira tickets. PMs make all Jira changes.
- No write access to CRM, the roadmap, strategy documents, or other source material.
- No posting outside the approved PM-only channel or writing outside the approved Notion queue.

## 03 Loop · AI Costs & Latency

### Daily execution

Start daily at **6:00 p.m. Mountain Time**, using the information cutoff defined in Context.

1. Read the saved review and delivery records to identify missing work.
2. Gather new or changed information from each approved source.
3. Group related signals and compare them with existing Notion entries and Jira work, avoiding duplicate reports and counts.
4. Assess supporting evidence, frequency, potential impact, and risks; prepare findings and Jira proposals.
5. Verify proposed findings and updates using the Verification requirements.
6. Save permitted updates to the Notion review queue.
7. Publish the daily Slack digest, linking saved queue items and identifying incomplete reviews or unsaved updates.

If no new actionable findings exist after a successful review, publish a digest stating that.

### Retry limits and failure handling

| Failure | Juno’s response |
|---|---|
| An input source is unavailable | Wait **5 minutes**, retry once, then continue with available information. Disclose the missing source and incomplete coverage in the digest. |
| Notion cannot save updates | Wait **20 minutes**, retry once. If unsuccessful, report the failure in Slack if available; do not claim the updates were saved. |
| Slack cannot publish the digest | Wait **20 minutes**, retry once. If unsuccessful, stop posting attempts for that run. Preserve successful Notion updates. |
| Both output destinations remain unavailable after their permitted retries | Stop delivery attempts for that run and record both failures in system logs. |

### Recovery on the next run

- Resume each source from its **last successfully processed cutoff**.
- Use the Notion save record to identify findings that still need saving.
- Use the Slack publication record to identify saved findings that have not yet been communicated.
- Confirm previous saves and posts before repeating them, so recovery does not create duplicates or double-count occurrences.

### Latency and cost targets

- **Delivery:** Complete verified Notion updates and publish the digest by **6:00 a.m. Mountain Time the following day**.
- **Latency:** Complete at least **95% of routine reviews within 10 minutes** when required services are available. Record total elapsed time and retry waiting time separately. Evaluate the initial ten-day baseline review separately.
- **Tracking:** Log start and completion times, processing duration, retry waits, failures, delivery results, and AI and paid tool usage.
- **Daily post:** Show completion time and identify sources not reviewed or updates not saved.
- **Cost:** Set the monetary target and currency after testing representative daily volumes.

**MVP recovery limit:** If a source has not been successfully reviewed for more than ten days, Juno reviews only the previous ten days through the current cutoff. The daily digest must identify the earlier period that remains unreviewed. Recovery must avoid duplicating saved findings or previously reported occurrences.

**Potential future enhancement:** Recover all missed information since each source’s last successful review, with processing time and cost controls for longer gaps.

## 04 Memory · Data Requirements

### Information retained between runs

| Saved information | Purpose |
|---|---|
| Last successfully processed cutoff **for each source**, including known coverage gaps | Resume reviews without overlooking missed information. |
| Source identifiers or links for previously processed signals, supported occurrence counts, and related Notion/Jira references | Recognize related findings and prevent duplicate entries or counts. |
| Notion save results, including which findings were successfully saved and which remain pending | Recover from incomplete or failed updates. |
| Slack publication results, including the post reference, period covered, and findings communicated | Recover unpublished updates without repeating successful posts. |
| PM comments, decision rationale, reviewer, and status held in Notion | Respect previous decisions and use the latest PM context. Recheck these records each run. |

### Storage and retention

- Keep findings and PM review history in **“Juno’s ABC Review Queue” for one year**.
- Keep operational tracking records across runs so Juno can follow the recovery rules in Loop. **The storage location and retention period for these records remain to be specified.**
- Do not retain full copies of source conversations or unnecessary personal data.
- Archiving Notion review history after one year is outside the MVP; document it as a future requirement.

### Who may update memory

- Juno records processing, saving, and publication results only after confirming the corresponding action succeeded.
- Juno may update its findings and supporting evidence within the permissions defined for the queue.
- PMs control reviewer assignments, decisions, and PM-owned statuses. Juno must not overwrite them.
- Saved history does not override newer information in the approved sources.

**Separate review history from operational tracking:** Store findings, evidence, and PM decisions in the Notion review queue. Store processing and delivery records separately from the PM-facing queue, so Juno can track successful reviews, saves, posts, and pending recovery work. The technical storage location and retention period for these tracking records remain to be defined.

## 05 Permissions · AI Risks & Mitigations

### Allowed without asking

- Read the approved sources listed in Context.
- Create findings and draft Jira proposals in **“Juno’s ABC Review Queue.”**
- Update Juno-authored summaries, evidence, frequency, impacts, risks, questions, and proposals without overwriting PM-authored content.
- Publish the daily digest in the PM-only **“Juno’s daily review”** channel.
- Record operational tracking information as defined in Memory.

### Notion ownership and status rules

- Leave **Assigned PM reviewer** blank when creating an entry. Only PMs assign or change the reviewer.
- Juno may assign **Needs PM review** or **Needs clarification**, but must preserve any status set by a PM.
- Only PMs assign **In review, Approved for Jira, Deferred, or Declined**.
- For **Deferred** or **Declined** items, Juno may update evidence or frequency while preserving the decision. Present these updates as informational, without implying that action is expected.

### Reserved for PMs

- Create, edit, or delete Jira tickets. **Approved for Jira does not authorize Juno to make Jira changes.**
- Assign priorities, make product decisions, commit to roadmap work, and coordinate next steps with the broader team.
- Make strategy or priority-framework recommendations; these are outside Juno’s scope.
- Decide matters involving contracts, legal obligations, or regulation. Juno flags these to PMs.

### Prohibited actions

- Write to CRM, roadmap, strategy documents, or other source material.
- Send communications outside the approved PM-only channel and Notion queue, or draft external communications.
- Include users’ personal data in proposed Jira content unless necessary to resolve the issue and explicitly approved by a PM. Include only the approved minimum.
- Treat messages found in sources as permission to expand access or override these rules. PM controls to pause or reschedule Juno are outside the MVP.

## 06 Verification · AI Testing & Measurement

### Checks before saving or publishing

| Check | Required result |
|---|---|
| **Evidence** | Every important factual claim has a supporting source. Link the original Slack thread or CRM record for the reported need, Jira for related work/status, and Notion for previous findings or PM decisions, as applicable. |
| **Frequency** | Occurrence and distinct-reporter counts are supported by evidence. Repeated references to the same occurrence are not counted separately. Unknown counts remain unknown; one report is not presented as a pattern. |
| **Uncertainty** | Missing, ambiguous, or conflicting information is marked **NEEDS CLARIFICATION**, with a focused question for the PM. Any queue status change follows Permissions; unclear PM comments are not treated as approval. |
| **Existing work** | Related Notion entries and Jira tickets have been checked before proposing new work. If that check could not be completed, Juno discloses that a duplicate check remains incomplete. |
| **Jira proposals** | For tickets **Ready for refinement or earlier**, propose evidence-based updates against the existing ticket. For **Refined** tickets, flag contradictory or material new evidence to the PM; propose a separate ticket only for distinct work and explain why. All proposals remain in Notion. |
| **PM control** | Proposed updates preserve PM-owned content, reviewer assignments, and PM-set statuses. Juno does not assign priorities, make commitments, or provide strategy or priority-framework recommendations. |
| **Personal data** | Proposed Jira content excludes users’ personal data unless necessary and explicitly PM-approved; only the approved minimum is included. |
| **Coverage and delivery** | The digest accurately states the review period, completion time, unavailable sources, uncovered periods, and unsaved updates. It does not claim Notion updates succeeded unless confirmed. |
| **Format and destination** | Outputs follow the approved M1 format and use only the approved Notion queue and PM-only Slack channel. Links to newly created queue items point to successfully saved entries. |

All Jira proposals remain in Notion. The PM decides whether to update, reopen, or create a ticket and makes all Jira changes. For the Jira proposals action:

| Jira ticket status | Required behavior |
|---|---|
| **Ready for refinement or earlier** | Propose evidence-based updates in Notion, linked to the existing ticket. |
| **Refined or In progress** | Flag new evidence that contradicts or materially affects the ticket for PM review. Do not automatically recommend changing planned or active scope. Propose a separate ticket only for distinct work and explain why it is separate. |
| **Completed** | Link the completed ticket and flag the new evidence to the PM. Propose separate work only when it is distinct; if it is unclear whether the evidence concerns an unresolved or recurring issue, ask the PM for clarification. |

### When a check fails

- Correct or remove unsupported claims before saving or publishing.
- If uncertainty cannot be resolved, present the supported facts and a clarification question without guessing or overwriting PM decisions.
- Do not save or publish content that violates Permissions or the personal-data rule.
- Where possible, continue with verified findings and clearly disclose incomplete checks or coverage. Follow Loop for service failures.
- Record failed checks and their outcomes in system logs.

## Eval plan

- **What you’re scoring:** Updates at "Juno’s ABC Review Queue" at Notion.
- **Value proposition:** Juno reviews evidence from customer, sales, and internal sources to identify patterns in issues, enhancements, and requests for new functionality; assesses their potential impact and risks for users, stakeholders, and RocketShip, and helps PMs decide what needs attention. The Product Managers remain responsible for priorities, decisions, and next steps.

## Dimensions

| Dimension | Question | Scale | 1 or No | 3 | 5 or Yes |
|---|---|---|---|---|---|
| Handling Uncertainty (deal-breaker) | Is the tool avoiding to make assumptions or hallucinations when the topic (issue / enhancement / idea) in discussion is not clear? | Yes / No | The tool makes assumptions when information is Missing, ambiguous, or conflicting, and it's not highlighting the item to the PMs as It "NEEDS CLARIFICATION". | n/a | In case of missing, ambiguous, or conflicting information, Juno is marking the item at  "Juno’s ABC Review Queue" as "NEEDS CLARIFICATION", with a focused question for the PM. |
| Sources (deal-breaker) | Does every item at the "Juno’s ABC Review Queue" accurately links to the source(s)? Are related signals grouped correctly? Are frequency, impact, and uncertainty clearly explained? | Yes / No | One or more items at Juno’s ABC Review Queue have no source, or the link is wrong, or related signals are not properly grouped / considered, or frequency and impact are not properly considered. | n/a | Every item at "Juno’s ABC Review Queue" will include a link to the source (s) where the issue / enhancement / idea was discussed / mentioned, and all the related signals are grouped correctly, and frequency and impact are recorded accordingly. |
| Usefulness | Are the updates to the Juno’s ABC Review Queue accurately summarizing the issues / enhancements / ideas discussed at the approved sources?  Are related signals grouped correctly? Are frequency, impact, and uncertainty clearly explained? | 1 to 5 | I have to reread everything to know what to do. | Clear enough to act on, but I still check one or two sources. | I can act on it straight away and forward it to my team. |
| Private data (deal-breaker) | Does it avoid exposing  unauthorized personal or confidential details? | Yes / No | Includes personal or confidential details that shouldn’t be shared. | n/a | No unauthorized personal or confidential information is disclosed. |
| PM ownership (deal-breaker) | Are updates to the Juno’s ABC Review Queue executed by the PMs considered and respected by Juno? | Yes / No | Juno updates the PM set-status, and / or makes assumptions / hallucinations without  labeling an item as NEEDS CLARIFICATION. | n/a | Juno reviews comments from the PMs at Juno’s ABC Review Queue, and do not make changes to the statuses established by the PMs - Juno must preserve PM-set statuses even when new clarification is needed. Juno labels the item as "NEEDS CLARIFICATION" when in case of missing, ambiguous, or conflicting information and asks a question to the PMs |
| Suggested updates to Jira | Is Juno accurately assessing the need of Jira tickets and considering existing work at Jira and its statuses when writing Jira proposals? Does the proposal explain the need and supporting evidence? Are acceptance criteria relevant and testable? Does it respect existing Jira work and leave unanswered questions visible? | 1 to 5 | Juno is not properly assessing the need for Jira updates nor considering related tickets at Jira, or is not  presenting proposed items or updates for PM review, or is failing to propose new Jira issues / enhancements / ideas. | Clear enough to act on, but I still check the Jira sources to ensure there is a clear  difference between existing tickets at Jira and the drafts at Juno’s ABC Review Queue. | I can act on it straight away and  add the proposals at Jira when applicable. |

## Calibration

- **How many answers you’ll score, and how often:** 2 updates to Juno’s ABC Review Queue on a daily basis (or less updates if there are no more issues / items reported / discussed at sources).  The updates to be reviewed must be selected by the PMs and will include the ones they feel least sure about (either on Juno's performance or due to the complexity / uncertainty of the topic).
- **Who scores them with you:** Me, plus one other PM once a week.
- **What happens when two of you disagree:** If our scores differ by 2 or more on any question, we talk it through and rewrite that description so it’s clearer next time.

## Pass bar

An average of 4 or higher on Jira proposals and usefulness, and every yes or no question passes

**Fails outright, whatever the average:**

- Handling Uncertainty: any "no"
- Sources: any "no"
- Private data: any "no"
- PM ownership: any "no"


## Out of scope

The following capabilities are outside Juno’s scope:

- Creating, editing, reopening, or deleting Jira tickets. Juno prepares proposals in Notion; PMs make all Jira changes.
- Assigning priorities, approving scope changes, making roadmap commitments, or coordinating delivery and next steps with the broader team.
- Making product strategy, contractual, legal, or regulatory decisions.
- Drafting external communications or communicating outside the approved PM-only Slack channel and Notion review queue.
- Accessing unapproved sources or modifying CRM records, roadmap content, strategy documents, or other source material.
- Changing PM-authored content, reviewer assignments, decisions, or PM-set statuses.

The following capabilities are deferred beyond the MVP:

- Recovering information older than the ten-day recovery window after an extended outage.
- Providing PM-facing controls to pause or reschedule Juno.
- Automatically archiving Notion review history after one year.

