# Managed agents

AgentMail gives agents email inboxes. We want customers to be able to create and operate agents on top of that infrastructure without building and hosting a separate service for each one.

## The problem

Customers have different jobs for agents to do. Today, getting one running involves more than describing the task: someone needs to connect its inputs and tools, run it, retain its state, and make its work understandable.

We want a shared product and backend that handles those responsibilities so a customer can create an agent by configuring its behavior.

## Who is the customer?

Build for someone configuring and operating email agents for their team or customers. They know the job they want done and need a product that handles the setup and execution. Different users will bring different instructions, context, and workflows. For example:

- A billing agent might process invoices and CC the appropriate people.
- A support agent might investigate an incoming issue and identify which engineer to CC.

These illustrate different uses of the same infrastructure. The product should support customer-defined behavior through configuration and the supplied harness, without changes to application code for each use case.

Rho, an AgentMail customer whose team wants to create agents for its customers, is one example of this need. The platform should work across customers and use cases.

The [example scenarios](fixtures/company.md) and inputs are synthetic. They are starting configurations to try, not business rules to hardcode into the product.

## What we'd like you to build

Build a managed-agent product where someone can **create an agent, define its behavior, run it, and inspect its work**.

The user should be able to:

- Create agents with different instructions and connect them to provided inputs and tools.
- Run an agent on a supplied input through the execution harness.
- Understand its progress, inspect its input, output and tool activity, and see when execution fails.
- Return later and find saved agents and their results.

Demonstrate two differently configured agents using the same creation, execution, and inspection flow. Billing and support are supplied examples; neither requires a separate screen, API, or business-specific implementation.

The user should also be able to update an agent's configuration, leave while work runs in the background, and return to inspect its run history.

## Scope

Build a working Next.js frontend and backend with application data persisted in Postgres. You own the configuration experience, schema, APIs, validation, background execution, and execution integration.

Processing should continue independently of an open browser. Decide what happens when an input arrives again, execution is interrupted, or someone wants to retry. Implement a coherent approach within the available time and make its limitations clear. The retry policy, controls, and data model are yours to design.

Keep the infrastructure bounded: one customer workspace, email as the input type, and the supplied harness and toolset are enough. Arbitrary-code hosting, a visual workflow builder, new tool integrations, authentication, and deployment are outside scope. Record external actions through local stubs; do not send real email or execute payments.

## Questions to consider

- What does a customer need to configure to create a useful agent? What can be handled for them?
- Which concepts belong to the shared platform, and which belong in an agent's configuration?
- How can someone understand what an unfamiliar agent did and whether it succeeded?
- How does your system behave if an input arrives twice or an execution is retried?
- What should happen when an agent's instructions or available tools change?
- Can another use case fit without changing the application's schema or adding a dedicated workflow?

## Working together

Start by exploring the examples and sketching a user flow and technical approach. We'll discuss them together, then you will spend most of the session building.

Use us as teammates: ask questions, challenge assumptions, and tell us when something blocks you. Before the end, we'll have someone try the product so you can observe it and make an adjustment.

At the end, show the working experience and walk through the decisions behind it. Keep brief [design notes](DECISIONS.md) and the commands needed to run and check your work. You may use AI tools, libraries, and existing components; be ready to explain and modify what you build.

## Development environment

Use Next.js and TypeScript, Postgres, and the supplied local execution harness. We provide the starter, database access, model access, example inputs, and tools. You choose the application architecture.

See [setup](docs/SETUP.md) and [the harness contract](docs/HARNESS.md) for their preparation status. Keep credentials on the server and out of source control.
