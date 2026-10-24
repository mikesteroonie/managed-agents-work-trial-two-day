# Local setup

The runnable starter is still being prepared by the AgentMail team. This repository currently contains the product brief and scaffolding placeholders. The team will complete and verify the starter before the work trial.

We provide a Next.js console shell with a Managed Agents sidebar destination, an assumed logged-in user and workspace, a configured server-side AgentMail SDK client and credentials, an empty Postgres database, and the local execution harness with model access.

You build the agent builder and its backend, use the supplied client to integrate with AgentMail, and implement webhook registration, intake/validation, and local replay tooling. See the [AgentMail integration guide](AGENTMAIL.md) for the relevant endpoints and replay explanation.

The team will add exact installation, environment configuration, client import/example, start, database connection, and harness-check commands here. Local replay is sufficient for testing; cloud deployment is not required.

Once you add application migrations and checks, document how to run them here or in [design notes](../DECISIONS.md).
