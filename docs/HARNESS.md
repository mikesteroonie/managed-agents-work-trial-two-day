# Local agent execution

The AgentMail team will provide a local execution harness and document its tested interface before the trial. It supplies model execution, predictable test modes, and a way to record proposed external actions locally.

The team will document the fixed model and available AgentMail tool capabilities. You implement the tool bindings using the supplied AgentMail client; model selection and tool-permissions settings are outside the product scope.

## Shared execution contract

The harness accepts agent configuration, email input/context, and tool bindings. It emits execution events, tool activity, and a result or failure. Instructions and result content come from the user-defined agent; there are no preset business workflows.

The harness runs locally and may call a hosted model with supplied credentials. Its test modes cover success, delay, tool activity, and failure. Use local action recording when testing generated email actions.

You own application storage, execution coordination, duplicate handling, and retry behavior. Follow your README's execution requirements; no separate worker or job system is supplied or prescribed.

## AgentMail integration

AgentMail is the only connector. The [integration guide](AGENTMAIL.md) lists the existing endpoints and explains local event replay.

Use the supplied client for inbox/message access and your tool bindings. You own webhook registration, the receiving endpoint, signature verification, payload validation, and inbox-to-agent routing. Incoming events must trigger the harness through your backend without a UI Run action.
