# Agent execution

The AgentMail team is preparing the local execution adapter. Its tested interface and examples will be added before the trial.

The harness accepts agent instructions, an incoming invoice email, and the supplied customer routing context. It returns invoice information, a proposed reply, and CC recipients, or an execution failure. Its exact typed contract will be documented here.

It runs locally and may call a hosted model with supplied credentials. Any email action uses a local recording stub; it never sends real email.

The adapter will provide repeatable success, delay, and failure scenarios as well as real model execution. Application persistence, execution coordination, duplicate handling, and retry policy belong to the candidate's application.

## Example email format

The files in fixtures/emails are synthetic normalized inputs for the exercise, not AgentMail's public webhook schema.

Each includes event_id, message_id, inbox_id, thread_id, received_at, from, to, subject, and text. Inbox and contact addresses are fictional. Invoice content is already text; no PDF parser is required.

The correction email is a new event in the same thread and repeats the invoice details. Replaying a file resends the same event. Decide how your product should represent those situations.
