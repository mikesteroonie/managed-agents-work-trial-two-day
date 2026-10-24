# Managed email agents

Rho is an AgentMail customer. People on their team want to create email agents for their customers without having to build and host the surrounding agent infrastructure.

## The problem

A billing agent could read an invoice and bring the right people into its email thread. A support agent could identify which engineer to CC. The model is one part of that experience: someone still has to configure the agent, connect its inbox, and understand what it did.

We want to make that experience usable as a product.

## Who is the customer?

Build for a person on Rho's team setting up an agent for a customer. They know the workflow they want, but should not have to write and operate an agent service to get it running.

For this project, focus on a **billing agent that processes incoming invoices and identifies the people to CC in the thread**. The included [customer scenario](fixtures/company.md), invoice emails, and routing contacts are synthetic examples, not real Rho policies or customer data.

## What we'd like you to build

Build the first version of a managed email agent experience: **configure an agent, process an invoice email, and understand its proposed action.**

The user should be able to:

- Create an agent with instructions and a connection to a provided inbox.
- Process an incoming invoice email using the supplied execution harness.
- Inspect the invoice information, proposed reply, and selected CC recipients alongside the original email.
- Understand what is happening and when execution has failed or needs attention.
- Return later and find the saved configuration and results.

The user should also be able to update the agent's instructions, leave while emails are processed in the background, and return to inspect its run history.

## Scope

Build a working Next.js frontend and backend with application data persisted in Postgres. You own the schema, APIs, validation, background execution, and experience.

Processing should continue independently of an open browser. Decide what happens when an event arrives again, execution is interrupted, or someone wants to retry. Implement a coherent approach within the available time and make its limitations clear. The retry policy, controls, and data model are yours to design.

Use one customer workspace and the supplied invoice text; PDF extraction, payment execution, authentication, and deployment are outside scope. Produce a draft or record a simulated email action with the chosen CC recipients. Do not send real email. The support-agent example is context for discussing generalization, not another workflow to build.

## Questions to consider

- What does the person setting up this agent need to know, and what should happen automatically?
- What would make them trust that the invoice reached the right people?
- What should the product do when the owner is unclear or the invoice changes?
- How does your system behave if the same event arrives twice or an execution is retried?
- Which information belongs in the interface, and which belongs in diagnostic detail?
- What would carry over to a support agent that identifies an engineer to CC?

## Working together

Start by exploring the examples and sketching a user flow and technical approach. We'll discuss them together, then you will spend most of the session building.

Use us as teammates: ask questions, challenge assumptions, and tell us when something blocks you. Before the end, we'll have someone try the product so you can observe it and make an adjustment.

At the end, show the working experience and walk through the decisions behind it. Keep brief [design notes](DECISIONS.md) and the commands needed to run and check your work. You may use AI tools, libraries, and existing components; be ready to explain and modify what you build.

## Development environment

Use Next.js and TypeScript, Postgres, and the supplied local execution harness. We provide the starter, database access, model access, and synthetic inputs. You choose the application architecture.

See [setup](docs/SETUP.md) and [the harness contract](docs/HARNESS.md) for their preparation status. Keep credentials on the server and out of source control.
