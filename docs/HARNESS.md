# AgentMail events and agent execution

The AgentMail team is preparing the local execution adapter. Its tested interface and examples will be added before the trial.

## AgentMail integration

AgentMail is the only connector. Incoming `message.received` events for a connected inbox are the primary trigger. The supplied adapter provides AgentMail inbox/message access and email tools; other service integrations are outside scope.

The team will provide a server-side AgentMail API client with a real API implementation and an interchangeable local simulator, plus webhook delivery/replay examples verified against the current AgentMail event contract. The simulator avoids live email delivery and public tunnels during iteration while exercising the same integration contract. Outbound email actions are recorded locally.

The candidate owns the application's backend event intake, inbox-to-agent association, execution integration, and persistence. A replayed event must follow that same intake path and trigger an agent without a UI Run action. The supplied integration adapter handles protocol details; it does not choose which configured agent to run or manage application run state.

## Shared execution contract

The harness accepts an agent's configuration (instructions, supplied context, and available tools) plus an input. It emits execution events and a final result or failure. The same contract must work for different agent purposes.

Document the generic event and result types, including tool calls and their outcomes. Output content is determined by the configured agent; invoice fields, reply drafts, and CC recipients are example content, not mandatory fields in every run.

The harness runs locally and may call a hosted model with supplied credentials. Provided tools record external actions locally instead of sending real email or executing payments.

Supply repeatable success, delay, tool-activity, and failure scenarios as well as real model execution. The harness does not provide the application's configuration storage, run database, background coordination, duplicate handling, or retry policy.

## Example inputs

The JSON files in fixtures/emails are synthetic normalized scenario data, not AgentMail's public webhook schema. Each includes event_id, message_id, inbox_id, thread_id, received_at, from, to, subject, and text. Before the trial, the team will add verified webhook envelopes and API responses around these scenarios and document their normalization into harness inputs. Do not present the current fixture shape as the production event format.

The [scenario file](../fixtures/company.md) contains billing and support configuration examples. Their inputs use different inboxes, but both go through the same harness. Replaying a file resends the same event. No PDF parser or application-specific email classifier is required.
