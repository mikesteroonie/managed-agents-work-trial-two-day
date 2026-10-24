# Local agent execution

The AgentMail team will provide a local execution harness and document its tested interface before the trial. It owns the model/tool loop, tool dispatch and error feedback, execution limits, and configured recovery within the loop. It also supplies predictable test modes and local recording of proposed external actions. This is a local execution abstraction, not a recreation of all AgentCore services.

The team will document the fixed model and available AgentMail tool capabilities. You implement the tool bindings using the supplied AgentMail client; model selection and tool-permissions settings are outside the product scope.

## Shared execution contract

The harness accepts agent configuration, email input/context, and tool bindings. It emits activity and an explicit final success or failure outcome. A tool error is intermediate activity: the loop may recover and still succeed. Use the final outcome to determine run status. Instructions and result content come from the user-defined agent; there are no preset business workflows.

The harness runs locally and may call a hosted model with supplied credentials. Its test modes cover success, delay, tool activity, and terminal failure, including failure after some recorded activity. Use local action recording when testing generated email actions.

Use the terminal-failure mode to implement the experience required in the README. You own invocation, application storage, presentation of the outcome, and the customer's next step. Any optional action to start another run is an application decision; retries and recovery inside the supplied loop are not your responsibility. Automatic crash recovery and concurrent duplicate-delivery guarantees are not required; no worker or job system is supplied or prescribed.

## AgentMail integration

AgentMail is the only connector. The [integration guide](AGENTMAIL.md) lists the existing endpoints and explains local event replay.

Use the supplied client for inbox/message access and your tool bindings. You own webhook registration, the receiving endpoint, signature verification, payload validation, and inbox-to-agent routing. Incoming events must trigger the harness through your backend without a UI Run action.
