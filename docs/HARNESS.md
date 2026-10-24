# Local agent execution

The AgentMail team will provide a local execution harness and document its tested interface before the trial. It supplies model execution, predictable test modes, and a way to record proposed external actions locally.

## Shared execution contract

The harness accepts agent configuration, email input/context, and tool bindings. It emits execution events, tool activity, and a result or failure. Instructions and result content come from the user-defined agent; there are no preset business workflows.

The harness runs locally and may call a hosted model with supplied credentials. Its test modes cover success, delay, tool activity, and failure. Use local action recording when testing generated email actions.

You own application storage, execution coordination, duplicate handling, and retry behavior. No separate worker or job system is supplied or prescribed.

## AgentMail integration

AgentMail is the only connector. Use the existing API or SDK with the provided credentials for inbox/message access and the [existing webhook service](https://docs.agentmail.to/webhooks-overview) for incoming email events.

You own webhook registration, the receiving endpoint, parsing and validation, inbox-to-agent routing, and any AgentMail tool bindings used by the agent. Use the documented signature-verification mechanism for received HTTP webhooks. You are consuming AgentMail's service, not rebuilding its webhook delivery infrastructure.

## Local event testing

Create your own synthetic webhook payloads matching the documented AgentMail event contract and a local delivery/replay script targeting your receiving endpoint. Account for verification in your local test setup and document how it works.

Replay should exercise the same event-handling path as live delivery and trigger execution without a UI Run action. Local replay does not require a public tunnel. To receive live HTTP deliveries, register a reachable endpoint using the [webhook API](https://docs.agentmail.to/api-reference/webhooks/create). Cloud deployment is not part of the trial.
