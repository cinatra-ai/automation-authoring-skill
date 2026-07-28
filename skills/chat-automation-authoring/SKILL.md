---
name: chat-automation-authoring
description: Use when the user wants to set up automation from chat — create an email outreach campaign, run one through the email-outreach orchestrator agent, create a scheduled trigger or recurring task, or create/revise/ask about a one-off dated WORKFLOW DRAFT/INSTANCE on the Gantt. Routes to the folded bundle's instructions and carries the rules they share. NOT for building a reusable workflow extension PACKAGE — that is chat-workflow-extension-authoring.
metadata:
  # cinatra-watches: the union of the four folded bundles' watches (cinatra#188;
  # flagged by the CI gate on change) — the campaign-create primitive base and
  # the canonical email-outreach agent workspace route (create-campaign), the
  # dispatch primitive + email-outreach orchestrator package
  # (chat-campaign-creation), and the workflow draft/template/status primitives
  # (chat-workflow-authoring).
  cinatra-watches:
    primitives:
      - email_outreach
      - agent_run
      - workflow_draft_create
      - workflow_draft_update
      - workflow_draft_get
      - workflow_draft_list
      - workflow_preview
      - workflow_validate
      - workflow_template_instantiate
      - workflow_template_list
      - workflow_status_get
      - workflow_status_list
    routes:
      - /agents/cinatra-agents/email-outreach/new
    packages:
      - "@cinatra-ai/email-outreach-agent"
---

You set up Cinatra automation from chat: email outreach campaigns, scheduled
triggers, and one-off workflow drafts. Pick the flow the request is in, follow
that flow's instructions, and apply the shared rules below to every flow.

## Pick the flow

- **Campaign creation** — the user asks to create a new outreach campaign,
  build a cold email sequence, or set up automated email outreach: create the
  campaign, then hand off to the email outreach agent workspace. Follow
  [Create campaign](references/create-campaign.md).
- **Chat campaign flow** — the user wants an email outreach campaign run from
  chat: dispatch the email-outreach orchestrator agent and let its HITL gates
  walk the user through it. Follow
  [Campaign creation rules](references/chat-campaign-creation.md).
- **Trigger creation** — the user asks to create a scheduled trigger, set up an
  automation, or run a recurring task on a cron schedule. Follow
  [Create scheduled trigger](references/create-trigger.md).
- **Workflow authoring** — the user wants to create, draft, revise, or ask
  about a one-off WORKFLOW DRAFT/INSTANCE: a concrete, dated, calendar-driven
  plan on the Gantt, anchored to a specific target date. Follow
  [Chat workflow authoring](references/chat-workflow-authoring.md).

## Shared rules (every flow)

- There is ONLY ONE campaign type: email outreach (`campaignTypeId`
  `campaign-email-outreach`). Never ask the user to choose or confirm a
  campaign type — it is implied.
- Workflow drafts are proposal-only: you create and revise DRAFTS and answer
  read-only status questions; you NEVER start, approve, or reject a workflow —
  those happen on the Gantt, by a human.
- A reusable, versioned, shippable workflow extension PACKAGE is a different
  deliverable from a one-off draft — that is the
  `chat-workflow-extension-authoring` skill, not this bundle. When ambiguous,
  ask: *"A reusable workflow package, or a one-off plan for a specific date?"*
