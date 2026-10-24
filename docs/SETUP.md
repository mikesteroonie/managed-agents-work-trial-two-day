# Local setup

The runnable starter is still being prepared by the AgentMail team. This repository currently contains the product brief and scaffolding placeholders. The team will complete and verify the starter before the work trial.

We provide a Next.js console shell with a Managed Agents sidebar destination, an assumed logged-in user and workspace, AgentMail API credentials, an empty Postgres database, and the local execution harness with model access.

You build the agent builder and its backend, integrate with AgentMail's existing API and webhook service, and create the webhook parsing/validation and local delivery/replay tools. Use your own synthetic event payloads based on the documented AgentMail contract. A custom API simulator is not required.

Exact installation, credential configuration, start, database connection, and harness-check commands will be added here. Local event replay should let you test your receiver without a public tunnel. Live HTTP webhook delivery requires a reachable URL; cloud deployment is not required for the trial.

Once you add application migrations and checks, document how to run them here or in [design notes](../DECISIONS.md).
