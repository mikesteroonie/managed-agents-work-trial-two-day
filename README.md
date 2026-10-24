# Managed agents

AgentMail gives agents email inboxes. We want customers to create agents that work with incoming email without building and hosting a separate service for each one.

## The problem

Customers know the job they want an agent to do, but getting it running also requires connecting an inbox, executing instructions, retaining state, and understanding what happened. Build a **Managed Agents** section in the AgentMail console that handles that setup and operation.

Build for someone creating email agents for their team or customers. Rho, whose team wants to create agents for its customers, is one example. The product should support different instructions and use cases without application-code changes for each one.

## What we'd like you to build

Assume the user is already logged in and has an AgentMail workspace, inboxes, and API credentials. Managed Agents belongs in the existing console sidebar. **AgentMail is the only connector; incoming `message.received` events trigger the agents.**

Keep configuration to three inputs:

- **Name:** a label for finding the agent later.
- **Instructions:** one Markdown document containing the task and useful context. Support writing or pasting text; importing an `.md` file is optional.
- **Inbox:** one existing AgentMail inbox whose incoming emails trigger the agent.

The model and available AgentMail tools are fixed for the trial. Make their capabilities understandable without adding settings for them.

### Frontend

- Create and save an agent with those three inputs.
- List saved agents and reopen their configuration. Show the linked inbox, pause state, and execution status.
- Edit and save the instructions/context of an existing agent.
- Pause and resume an agent, making clear when these changes take effect.
- Browse run history and inspect a run's input, status, output, tool activity, errors, and the configuration used. Retain everything after refresh.

Two customer requests should work through this interface:

- **“Our escalation contact changed.”** Save revised instructions so future emails use the new contact, while earlier results remain understandable.
- **“Stop this agent while I fix it.”** Pause new executions, change the instructions, then resume.

### Backend

- Build application APIs and a Postgres schema to create, list, and retrieve saved agents and their run data. You choose the route structure, validation, tables, and relationships.
- Use the supplied AgentMail client for inbox/message access and agent tool bindings. Implement webhook registration, the receiving endpoint, event parsing/validation, and inbox-to-agent routing using AgentMail's existing services.
- Trigger the supplied execution harness from incoming events and persist results, status, tool activity, and failures for the UI. Execution must not depend on someone pressing Run.

- Implement backend updates for an existing agent's instructions and persisted pause/resume state. New events after a saved edit use the updated configuration; keep past runs attributable to the configuration they used.
- Enforce pause in the backend: no new executions start while paused. Choose and explain what happens to queued work, active runs, and emails arriving during the pause.
- Execute in the background: acknowledge incoming HTTP events before the agent finishes, and continue working when the browser closes. You choose the execution mechanism; a separate worker or queue is not prescribed.

Decide how repeated events, interrupted execution, and retries should behave; implement a coherent approach and explain its limits.

Create synthetic payloads matching the documented webhook contract and a small local replay script that posts them to your receiving endpoint. It should exercise the same event-handling path as live delivery. Local replay is sufficient for the demo; see the [AgentMail integration guide](docs/AGENTMAIL.md) for endpoints and testing details.

## What we provide

Next.js/TypeScript and a console shell, an empty Postgres database, a configured **server-side AgentMail SDK client**, trial credentials, and a local execution harness with model access and predictable test modes. Use the harness's local action-recording mode when testing generated email actions.

You own the product screens, application APIs, schema, event handling, and execution integration. The [setup guide](docs/SETUP.md), [AgentMail endpoint guide](docs/AGENTMAIL.md), and [harness contract](docs/HARNESS.md) describe the starter and its preparation status. Keep credentials server-side and out of source control.

## Boundaries

Keep this to one existing workspace and email agents. Authentication, additional connectors, model settings, tool-permission editors, document management, arbitrary-code hosting, workflow builders, and cloud deployment are outside scope. Use AgentMail's existing webhook service; do not build a delivery service.

Version-comparison screens, rollback, inbox reassignment, backlog management, and cancellation of running work are not required.

## Questions to consider

- How will someone understand what the agent can do and when it runs?
- What should they see first when inspecting a result or failure?
- Can different instructions work through the same product and data model?
- How do edits, pause/resume, and repeated events affect work already in progress?

## Working together

Start with a sketch of the user flow and technical approach. Discuss it with us, then spend most of the trial building. Ask questions and surface blockers as you go.

Demonstrate different user-defined instructions through the same creation, email-triggered execution, and inspection flow. We'll have someone try the product so you can observe it and make an adjustment.

Keep brief [design notes](DECISIONS.md) and commands for running and checking your work. AI tools and existing components are welcome; be ready to explain and modify what you build.
