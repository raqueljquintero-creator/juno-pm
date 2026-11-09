# Prototype · Juno

> Module 2 · Prototype. The working build that tests your idea, made with your build tool of choice.

## Prototype link

The public share URL from Lovable: https://juno-insight-digest.lovable.app 

_____

## What it demonstrates

_**Who’s using it**_

RocketShip ABC Product Managers are Juno’s users. They receive one daily review based on new or changed information from three Slack channels, the ABC Jira dashboard, the ABC product roadmap, and Juno’s ABC Review Queue in Notion. Juno checks the first 10 days of information to establish a baseline; on later runs, it reviews changes since the last successful review, including PM comments and decisions.

_**Where you’d see it**_

**In Slack:** 
Once a day, Juno posts a summary in the PM-only “Juno’s daily review” channel. It highlights new issues, enhancement ideas, and requests for functionality; new evidence about items already in the Notion queue or Jira; and risks or questions that may need PM attention. It gives the evidence and rationale for its recommendations, but leaves final priorities to the PMs. The post includes the review period, links to sources and related queue items, and PM comments or decisions incorporated since the previous review. If there are no new actionable items, it says so.

At the end of the post, a “Open Juno’s ABC Review Queue” button links to the Notion queue.

**In Notion:** The PM-only “Juno’s ABC Review Queue” holds the detailed summaries, source links, frequency, potential impact, related Jira item and status, recommendations, and any draft Jira content. The PM reviewer field is blank until a PM takes ownership. Juno can set the review status to Needs PM review or Needs clarification. PMs control the other statuses and decisions; Juno does not change a status after a PM sets it.

_**What it takes off your plate**_

Juno reduces the time PMs spend reading the three Slack channels, checking Jira and the roadmap, and searching the Notion queue for related evidence or prior decisions. It brings relevant signals together, shows when new reports relate to existing work, and makes it visible when a PM has taken ownership. PMs can spend less time searching and reconciling context, while keeping control of priorities, decisions, communications, and Jira changes.


_____

## Debrief


- **What worked:**

   The prototype showed the daily review in Slack and linked to more detailed information in the Notion review queue. The Notion view also included filters, and the mock data showed reports from previous days.

- **What broke / felt like a toy:**

   The Slack post included an “Acknowledged” button that wasn’t requested. After discussing it with a peer, we couldn’t identify a clear user need for it, so I removed it.

- **What I’d change next pass:**

   Make the report easier to scan and more visually appealing. It currently feels busy, so I’d improve the visual hierarchy and reduce clutter.
