# Local setup

The runnable starter is still being prepared by the AgentMail team. This repository currently contains the product brief, synthetic inputs, and scaffolding placeholders. The team will complete and verify this setup before the work trial.

The prepared environment will include a Next.js console shell with a Managed Agents sidebar destination, an assumed logged-in user and workspace, an empty Postgres database, local agent execution, and model access.

The AgentMail integration will include an API adapter for the supplied inboxes/messages and tools, plus local webhook delivery/replay. AgentMail is the only connector. Replayed incoming-email events must reach the application's backend event intake; local iteration must not require a public webhook URL or AWS deployment. Authentication and the surrounding console are supplied context, not candidate build tasks.

Exact installation, environment configuration, start, database connection, and harness-check commands will be added here. You should not need to create a cloud account or deploy to AWS.

Once you add application migrations and checks, document how to run them here or in [design notes](../DECISIONS.md).
