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

- **Required sources:**_
    -    The approved Slack channel where stakeholders and PMs discuss user issues, enhancements, and ideas: "ABC PMs Only"._
    -    The approved Slack channel where technology teams discuss ABC product issues in production or lower environments: "Rocketship Prod issues and highlights".
    -    The approved Slack channel where the ABC delivery team and PMs discuss production issues: "ABC Prod today".
    -    The approved Slack Channel to post Juno's daily review: “Juno’s daily review”.
    -    The "ABC Jira dashboard".
    -    The "ABC Product Roadmap".
    -    The Notion review queue which includes PM comments and decision statuses: “Juno’s ABC Review Queue”.
    -    The sales pipeline pulled from CRM, including customer needs, blockers, and sales commitments: "Sales pipeline snapshot".
    -    The "Product Strategy One-Pager" to give context about the Vision of the Rocketship ABC product.

- **Deliberate exclusions:** 
    -    The "Engineering capacity Note" is not relevant for the Juno's review since all the capacity limitations and its connection with the priorities are be handled by the product managers.
    -    Access to emails since not all the information included there will be relevant for Juno. The PMs will bring it to the allowed channels if applicable.
    -    Access to other Slack channels, since the information relevant to Juno is included at the list of approved channels mentioned above.
- **SLA of truth:**
    -    All the information at the approved sources by the end of the day must be considered as part of the "Juno's daily review". If more information is required to confirm a change in direction Juno may label the existent / new item to the status "Needs PM review" or "Needs clarification". 
- **When a source is unreachable:**
    -   If a source is unavailable, Juno waits five minutes, retries that source once, and then continues the review. If it remains unavailable, Juno notes the source and issue in the daily report and makes clear that the review may be incomplete.

## 02 Tools · System Capabilities

- **The verb list:**
    -   READ the required sources at the end of the day.
    -   DRAFT findings, evidence, frequency updates, risks, questions, and proposed Jira content to the “Juno’s ABC Review Queue”.
    -   WRITE a daily summary and links to relevant queue items in “Juno’s daily review”. 
- **Deliberate omissions:**
    -   DO NOT  create, edit, or update Jira tickets. All Jira suggestions remain in the Notion queue (“Juno’s ABC Review Queue”) for PM review. The daily Slack post at “Juno’s daily review” summarizes those suggestions; it does not make Jira changes. 

## 03 Loop · AI Costs & Latency
Juno follows this sequence:
  1. Gather new or changed information from the approved sources.
  2. Group related signals.
  3. Check the Notion queue and Jira for matching or previously reviewed work.
  4. Assess the evidence, frequency, impact, and risks.
  5. Update the Notion queue with findings or proposed Jira content.
  6. Verify the findings and post the daily Slack summary.

- **Turn ceiling:** _
   - If a source is unavailable, Juno waits five minutes, retries that source once, and then continues the review. If it remains unavailable, Juno notes the source and issue in the daily report and makes clear that the review may be incomplete.
   - If the “Juno’s daily review” is unavailable at the time to write the daily post, Juno waits twenty minutes, retries that source once. If it remains unavailable, Juno will stop trying and skip the daily report.
   - If the “Juno’s ABC Review Queue” is unavailable at the time to draft the updates, Juno waits twenty minutes, retries that source once. If it remains unavailable, Juno will stop trying  and mention the failure at the "Juno daily review" if this channel is available.
   - If the “Juno’s daily review” and the “Juno’s ABC Review Queue” are unavailable,  Juno will stop trying and skip the daily report and the daily updates.
   - If after reviewing the approved sources there are no new updates to report, indicate that at the “Juno’s daily review”.
- **Escalation trigger:**
   -  If after reviewing the approved sources there are no new updates to report, indicate that at the “Juno’s daily review”.
   -  If more information is required to report an update or new issue, Juno will label the existent / new item to the status "Needs PM review" or "Needs clarification".
- **Latency and cost target:** _e.g. p95 under 8s, under $0.12 per task._

## 04 Memory · Data Requirements

- **What persists, at what scope:** _turn, session, user, or team._
- **Expiry:** _TTL per fact._
- **Write rules:** _who outranks the model when a human disagrees._

## 05 Permissions · AI Risks & Mitigations

| Side-effect class | Tier |
|---|---|
| read | _auto / confirm / blocked_ |
| draft | _auto / confirm / blocked_ |
| write | _auto / confirm / blocked_ |
| send | _auto / confirm / blocked_ |

**Justification:** _blast radius and recoverability for each non-obvious tier._

## 06 Verification · AI Testing & Measurement

- **The check before output ships:** _what is checked, against what bar._
- **Failure behaviour:** _what happens when the check fails. Silently dropping the output is never the answer._

## Eval plan

_Stub. Module 5 fills this in: the human eval rubric in `05-evals/human-rubric.md`, with its pass bar._

## Out of scope

_Any capability not in the verb list, and any action tiered `blocked`. Both are decisions on the record, not omissions._
