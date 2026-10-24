# Agent execution

The AgentMail team is preparing the local execution adapter. Its tested interface and invocation examples will be added before the trial.

The harness accepts agent instructions, an incoming email, and the supplied company context. It produces a reply draft or an execution failure, with documented progress events where available. It runs locally and can call a hosted model using supplied credentials.

The adapter will include repeatable success, delayed-success, and controlled-failure scenarios alongside real model execution. Your application owns its data and the execution behavior described in the product brief.

## Example email format

The files in fixtures/emails are synthetic normalized inputs for this project, not the public AgentMail webhook schema.

Each includes event_id, message_id, inbox_id, thread_id, received_at, from, to, subject, and text. The inbox is defined in fixtures/inboxes.json. Messages can be treated independently; using conversation history is not required.
