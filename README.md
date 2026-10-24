# Managed agents

AgentMail gives agents email inboxes. We want customers to create agents that work with incoming email without building and hosting a separate service for each one.

## The problem

Customers know the job they want an agent to do, but getting it running also requires connecting an inbox, executing instructions, retaining state, and understanding what happened. Build a **Managed Agents** section in the AgentMail console that handles that setup and operation.

Build for someone creating email agents for their team or customers. For example, a platform team may create agents for its customers. The product should support different instructions and use cases without application-code changes for each one.

## What we'd like you to build

Assume the user is already logged in and has an AgentMail workspace, inboxes, and API credentials. Managed Agents belongs in the existing console sidebar. **AgentMail is the only connector; incoming `message.received` events trigger the agents.**

Keep configuration to three inputs:

- **Name:** a label for finding the agent later.
- **Instructions:** one Markdown document containing the task and useful context. Support writing or pasting text; importing an `.md` file is optional.
- **Inbox:** one existing AgentMail inbox whose incoming emails trigger the agent.

The model and available AgentMail tools are fixed for the trial. Make their capabilities understandable without adding settings for them. You choose the interaction flow, guidance, validation feedback, and how much detail to expose. Make setup and the latest outcome understandable without a narrated tour; decide what deserves emphasis and what to leave out.

### Frontend

- Create and save an agent with those three inputs.
- List saved agents and reopen their configuration. Show the linked inbox, pause state, and execution status.
- Edit and save the instructions/context of an existing agent.
- Pause and resume an agent, making clear when these changes take effect.
- Show the latest run's status, final output, any error, and confirmed actions completed before failure. Retain saved configuration and the latest result after refresh.

Two customer requests should work through this interface:

- **“Our escalation contact changed.”** Save revised instructions so future emails use the new contact.
- **“Stop this agent while I fix it.”** Pause new executions, change the instructions, then resume.

### Backend

- Build application APIs and a Postgres schema to create, list, and retrieve saved agents and their latest run data. You choose the route structure, validation, tables, and relationships.
- Use the supplied AgentMail client for inbox/message access and agent tool bindings. Implement webhook registration, the receiving endpoint, event parsing/validation, and inbox-to-agent routing using AgentMail's existing services.
- Trigger the supplied execution harness from incoming events and persist the latest run's status, final output, confirmed action outcomes, and any terminal error for the UI. Execution must not depend on someone pressing Run.

- Implement backend updates for an existing agent's instructions and persisted pause/resume state. New events after a saved edit use the updated configuration.
- Enforce pause in the backend: no new executions start while paused. Choose and explain what happens to queued work, active runs, and emails arriving during the pause.

AgentMail expects prompt acknowledgment and may retry delivery, so the same event can reach your endpoint more than once. For the local prototype, execution within the event-handler request is acceptable; explain the implications for live delivery. You choose the execution architecture; a separate worker or queue is optional.

Use the supplied replay script and signing helper to post sample events to your local receiving endpoint. Create payload variants to test your implementation. Local replay is sufficient for the demo; see the [AgentMail integration guide](docs/AGENTMAIL.md) for details.

### Product behavior

Anticipate edge cases and failure modes across setup, saving, execution, and interpreting results. Prioritize those that matter for this product, implement appropriate behavior, and explain any remaining limitations. Keep the customer experience consistent with what the backend knows.

The supplied harness owns the agent loop and recovery within it. You own the application around it, including how its outcomes are stored and presented. Use its confirmed action outcomes to show partial completion, such as a reply recorded before the run failed. Label test actions as recorded, and avoid implying that failed execution undid earlier actions. A concise latest-run summary is sufficient; no activity timeline or automatic run retry is required.

## What we provide

Next.js/TypeScript and a console shell, an empty Postgres database, a configured **server-side AgentMail SDK client**, an isolated trial workspace with its own inboxes and API key, and a local execution harness with model access and predictable test modes. Use the harness's local action-recording mode when testing generated email actions.

You own the product screens, application APIs, schema, event handling, and execution integration. The [setup guide](docs/SETUP.md) covers the planned starter and execution harness; the [AgentMail endpoint guide](docs/AGENTMAIL.md) lists integration points. Keep credentials server-side and out of source control.

## Boundaries

Keep this to one existing workspace and email agents. Authentication, additional connectors, model settings, tool-permission editors, document management, arbitrary-code hosting, workflow builders, and cloud deployment are outside scope. Use AgentMail's existing webhook service; do not build a delivery service.

Run history, configuration versioning, rollback, inbox reassignment, backlog management, and cancellation of running work are not required.

## Questions to consider

- How will you make creating and using an agent clear and pleasant? What should the user see and do at each step?
- What should a customer understand from the latest result, and which details would you leave out?
- Why do your data model and API boundaries fit this experience?
- Which edge cases matter most here, and what should the customer experience when they occur?

## Working together

Start with a sketch of the user flow and technical approach. Discuss it with us, then spend most of the trial building. Ask questions and surface blockers as you go.

Demonstrate different user-defined instructions through the same creation, email-triggered execution, and inspection flow. We'll have someone try the product so you can observe it and make an adjustment.

Keep brief [design notes](DECISIONS.md) and commands for running and checking your work. AI tools and existing components are welcome; be ready to explain and modify what you build.
