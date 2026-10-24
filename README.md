# Managed agents

AgentMail gives agents email inboxes. Build a **Managed Agents** section in the AgentMail console where customers can configure agents that respond to incoming email, without building and hosting a separate service for each one.

## The problem

Customers have different jobs for agents to do. Today, getting one running involves more than describing the task: someone needs to connect its inputs and tools, run it, retain its state, and make its work understandable.

We want a shared product and backend that handles those responsibilities so a customer can create an agent by configuring its behavior and connecting it to an AgentMail inbox. **AgentMail is the only connector for this trial:** use its API for inbox and message access, and its incoming-email events to trigger agents.

## Who is the customer?

Build for someone configuring and operating email agents for their team or customers. They know the job they want done and need a product that handles the setup and execution. Users supply their own instructions and context; the builder should support different email-agent behaviors without application-code changes for each use case.

Rho, an AgentMail customer whose team wants to create agents for its customers, is one example of this need. The platform should work across customers and use cases.

## What we'd like you to build

Build this as a **Managed Agents** destination in the sidebar of an existing console. Assume the user is already logged in, has API credentials, and has an AgentMail workspace with inboxes. Use the supplied console shell; focus on the agent builder and its backend.

Someone should be able to **create an agent, define its behavior, connect an inbox, and inspect the work triggered by incoming email**.

The user should be able to:

- Create and save agents with user-defined instructions, then connect them to an AgentMail inbox.
- Have an incoming AgentMail `message.received` event trigger the appropriate agent through the execution harness.
- Understand its progress, inspect its input, output and tool activity, and see when execution fails.
- Return later and find saved agents and their results.

Demonstrate the builder with different user-defined instructions through the same creation, event-triggered execution, and inspection flow. We do not provide preset agent configurations.

Use AgentMail's existing [API and webhook service](https://docs.agentmail.to/webhooks-overview). You own the API integration, webhook registration, receiving/parsing/validating events, and routing an event to the appropriate agent. Use the existing SDK or direct API calls; you do not need to build a webhook delivery service or a general API simulator.

Create synthetic webhook payloads that match the documented contract and a local delivery/replay script targeting your backend intake. Replays must exercise the same event-handling path as received webhooks. Local replay is sufficient for testing the receiver without a public tunnel; live HTTP webhook delivery requires a reachable URL. An event should start a run without someone pressing Run in the UI.

The user should also be able to leave while work runs in the background and return to inspect its run history. Handle these two customer requests:

1. **Change how an operating agent behaves.** “Our escalation contact has changed. Future emails should CC the new person, but I still need to understand what happened on previous emails.” Let the user update instructions or supplied context. New events received after saving should use the updated configuration. Decide what happens to already queued or running work, and make it possible to understand which configuration produced a past result.
2. **Pause an agent while fixing it.** “This agent is responding incorrectly. Stop starting new work while I fix the instructions, then let me resume it.” Provide pause/resume controls enforced by the backend. Decide what happens to emails received while paused and to executions already in progress, and explain that behavior in the product.

Keep these changes focused. A version comparison UI, rollback system, backlog management screen, and cancellation of running work are not required. You own the behavior and data model needed to make these two requests understandable and reliable.

## Scope

Build a working Next.js frontend and backend with application data persisted in Postgres. You own the configuration experience, schema, APIs, validation, background execution, and execution integration.

Accept incoming events and execute agents in the background, independently of both an open browser and the event's HTTP request. Do not hold that request open until the agent finishes. You choose how to run background work; a separate worker or queue is not prescribed. Decide what happens when an event arrives again, execution is interrupted, or someone wants to retry. Implement a coherent approach within the available time and make its limitations clear. The retry policy, controls, and data model are yours to design.

Keep the infrastructure bounded: one existing workspace, AgentMail inboxes and email events, and the supplied execution harness. AgentMail is the only connector. Other connectors, a connector marketplace, arbitrary-code hosting, a visual workflow builder, authentication, and cloud deployment are outside scope. Use the harness's local action-recording mode when testing generated email actions.

## Questions to consider

- What does a customer need to configure to create a useful agent? What can be handled for them?
- How does a user connect an inbox and understand which incoming emails will trigger their agent?
- Which concepts belong to the shared platform, and which belong in an agent's configuration?
- How can someone understand what an unfamiliar agent did and whether it succeeded?
- How does your system behave if an input arrives twice or an execution is retried?
- What should happen when an agent's instructions or available tools change?
- Can another use case fit without changing the application's schema or adding a dedicated workflow?

## Working together

Start by exploring the existing AgentMail API and sketching the builder's user flow and technical approach. We'll discuss them together, then you will spend most of the session building.

Use us as teammates: ask questions, challenge assumptions, and tell us when something blocks you. Before the end, we'll have someone try the product so you can observe it and make an adjustment.

At the end, show the working experience and walk through the decisions behind it. Keep brief [design notes](DECISIONS.md) and the commands needed to run and check your work. You may use AI tools, libraries, and existing components; be ready to explain and modify what you build.

## Development environment

Use Next.js and TypeScript, Postgres, and the supplied local execution harness. We provide the console shell with an assumed logged-in workspace, AgentMail API credentials, database access, model access, and harness documentation. You build the AgentMail integration and local event-testing tools. You choose the application architecture.

See [setup](docs/SETUP.md) and [the harness contract](docs/HARNESS.md) for their preparation status. Keep credentials on the server and out of source control.
