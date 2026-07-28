# Cinatra Automation Authoring Skill

The chat assistant's automation-authoring guidance in one router bundle: creating an email outreach campaign, running one through the email-outreach orchestrator agent, creating a scheduled trigger, and drafting a one-off, dated workflow on the Gantt. Consolidated from four bundles of @cinatra-ai/assistant-skills (cinatra#2090) — the router picks the flow, and each folded bundle's prompt is preserved verbatim under references/.

**Install:** Install `@cinatra-ai/automation-authoring-skill` in your Cinatra instance. Assistants that list the `chat-automation-authoring` slug in their skill bundle pick it up from the skills catalog.

**Usage:** Mounted into assistant conversations on demand — you do not invoke it directly. It routes a campaign, trigger, or workflow-draft request to the folded instruction set for that flow.

**Configuration:** None. The skill carries no credentials; the primitives, routes, and agents it instructs against are supplied by the host instance.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The router lives in `skills/chat-automation-authoring/SKILL.md`; the verbatim folded prompts live under `skills/chat-automation-authoring/references/`.

**Troubleshooting:** If the assistant cannot create campaigns, triggers, or workflow drafts from chat, the bundle is not mounted — check that the assistant's skill bundle lists `chat-automation-authoring`.

## Works with

- The Cinatra chat assistant skill bundle
- The email-outreach orchestrator agent, the campaign and trigger primitives, and the workflow draft tools of the host instance

## Capabilities

- Create an email outreach campaign and hand off to the email outreach agent workspace
- Dispatch the email-outreach orchestrator agent to run a campaign through its HITL gates
- Gather a scheduled trigger's purpose, schedule, and tools, and present the plan before building it
- Create, revise, validate, and preview one-off dated workflow drafts and hand off to the Gantt
- Answer read-only workflow status questions without ever starting or approving a workflow
