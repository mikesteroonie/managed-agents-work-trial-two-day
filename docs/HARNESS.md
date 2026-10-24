# Agent execution

The AgentMail team is preparing the local execution adapter. Its tested interface and examples will be added before the trial.

## Shared execution contract

The harness accepts an agent's configuration (instructions, supplied context, and available tools) plus an input. It emits execution events and a final result or failure. The same contract must work for different agent purposes.

Document the generic event and result types, including tool calls and their outcomes. Output content is determined by the configured agent; invoice fields, reply drafts, and CC recipients are example content, not mandatory fields in every run.

The harness runs locally and may call a hosted model with supplied credentials. Provided tools record external actions locally instead of sending real email or executing payments.

Supply repeatable success, delay, tool-activity, and failure scenarios as well as real model execution. The harness does not provide the application's configuration storage, run database, background coordination, duplicate handling, or retry policy.

## Example inputs

The JSON files in fixtures/emails are synthetic normalized inputs, not AgentMail's public webhook schema. Each includes event_id, message_id, inbox_id, thread_id, received_at, from, to, subject, and text.

The [scenario file](../fixtures/company.md) contains billing and support configuration examples. Their inputs use different inboxes, but both go through the same harness. Replaying a file resends the same event. No PDF parser or application-specific email classifier is required.
