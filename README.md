# Managed email agents

AgentMail gives AI agents email inboxes. We want to make it easier for a developer to put an email agent to work without building the surrounding application themselves.

## The problem

A working agent is only part of the experience. Someone still needs to configure it, give it an incoming email, understand what it produced, and figure out what happened when it failed.

We want to bring those pieces together into a product a developer can use with confidence.

## Who is the customer?

For this project, imagine the developer responsible for the support inbox at Northstar Desk, a small software company. They want an agent to prepare replies to customer emails using instructions they provide. They will review the drafts themselves.

They need a useful first result quickly, and enough context to decide whether they trust it. They should not have to read application logs to understand what happened.

We've included [company context and example instructions](fixtures/company.md), along with synthetic emails. These are starting points for understanding the customer. Ask us for more context as you work.

## What we'd like you to build

Build the first version of a managed email agent experience: **configure an agent, give it an incoming email, and inspect its work.**

The developer should be able to:

- Create an agent with a name, instructions, and a connection to a provided inbox.
- Process an example customer email and understand when work is underway.
- Read the generated reply draft alongside the email it responds to.
- See a clear failure state when execution does not succeed.
- Return later and find the saved agent and its completed or failed runs.

The developer should also be able to leave the browser while an email is processed, retry a failed run, and change the agent's instructions without losing the context behind earlier results.

## Scope

Build a working frontend and backend, with configuration and run outcomes persisted in Postgres. Validate the inputs your backend accepts. Use the supplied execution harness to produce the drafts.

Incoming work should be accepted and saved before execution finishes. Processing runs independently of the browser, and pending work remains processable after an application or worker restart. Receiving the same email event again should not create a second logical run.

A failed run can be retried, with its earlier attempt still inspectable. When instructions change, an earlier run should still identify the instructions it used. You decide how to represent these relationships.

Use one agent per inbox and the supplied synthetic emails. Real sending, authentication, billing, attachments, and deployment are outside this project. Automatic recovery from a worker dying during a model call is also outside scope; be ready to discuss that case.

## Questions to consider

Use these to shape your approach and our opening conversation. You do not need to write an answer to every question.

- What is the customer's actual goal, and how would they know this feature is helping?
- Which emails can the agent answer directly, and which need clarification or a person? How should that affect the experience?
- What does the customer need to configure before trying the agent? What can have a sensible default?
- What information helps someone judge a result, and what would just add noise?
- How do your choices about data, APIs, and execution support that experience?
- Which parts of your approach would carry over to another email use case? What would you keep specific to reply drafting?

## Working together

Start by exploring the examples and sketching a user flow and technical approach. We'll discuss them together, then you will spend most of the session building.

Use us as you would teammates: ask questions, challenge assumptions, and tell us when something blocks you. Before the end, we'll have someone try the product so you can observe where it works and where it needs an adjustment.

At the end, show us the working experience and walk through the implementation and tradeoffs. Keep brief [design notes](DECISIONS.md) and the commands needed to run and check your work. A formal presentation is unnecessary.

You may use AI tools, libraries, and existing components. Be ready to explain and modify what you build.

## Development environment

Use Next.js and TypeScript for the frontend, Postgres for application data, and the supplied local harness for agent execution. You choose the schema, data access library, application APIs, and interface.

We provide the starter, database access, model access, and synthetic inputs. See [setup](docs/SETUP.md) and [the harness contract](docs/HARNESS.md) for their current preparation status. Keep credentials on the server and out of source control.
