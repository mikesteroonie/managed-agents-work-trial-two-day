# Local setup

This repository contains only the trial brief and supporting documentation. The AgentMail team will build the runnable starter before the work trial.

We provide a Next.js console shell with a Managed Agents sidebar destination, an assumed logged-in user and workspace, a configured server-side AgentMail SDK client and credentials, an empty Postgres database, and the local execution harness with model access.

You build the agent builder and its backend, use the supplied client to integrate with AgentMail, and implement webhook registration, intake/validation, and routing. We supply the local replay script and signing helper. See the [AgentMail integration guide](AGENTMAIL.md) for details.

The team will add exact installation, environment configuration, client import/example, start, database connection, and harness-check commands here. Local replay is sufficient for testing; cloud deployment is not required.

Once you add application migrations and checks, document how to run them here or in [design notes](../DECISIONS.md).

## Execution harness

- The team supplies a local model/tool loop with funded model access and fixed tool schemas.
- It accepts instructions, email context, and your tool bindings; it returns final status, output, and any error.
- A client wrapper records outgoing actions in test mode; success, slow, and failure modes are supplied.
- You implement tool bindings, webhook integration, application execution state, database storage, and UI.
