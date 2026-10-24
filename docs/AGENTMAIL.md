# AgentMail integration

The team will supply a configured, server-side client built on the official AgentMail SDK, with credentials for the trial workspace. The starter will document its import path and a working inbox-list example. Keep credentials off the browser.

You build the application routes, tool bindings, webhook setup and intake, validation, and event-to-agent routing. AgentMail already provides the email API and webhook delivery service.

## Endpoints to consider

These are existing AgentMail endpoints, not routes you need to reimplement. Use the calls your flow needs.

| Purpose | Existing endpoint | Reference |
| --- | --- | --- |
| Select an existing inbox | `GET /v0/inboxes` | [List inboxes](https://docs.agentmail.to/api-reference/inboxes/list) |
| Read a triggering message | `GET /v0/inboxes/:inbox_id/messages/:message_id` | [Get message](https://docs.agentmail.to/api-reference/inboxes/messages/get) |
| Retrieve conversation context | `GET /v0/inboxes/:inbox_id/threads/:thread_id` | [Get thread](https://docs.agentmail.to/api-reference/inboxes/threads/get) |
| Register incoming-email delivery | `POST /v0/webhooks`, subscribing to `message.received` | [Create webhook](https://docs.agentmail.to/api-reference/webhooks/create) |
| Reply, including CC recipients when relevant | `POST /v0/inboxes/:inbox_id/messages/:message_id/reply` | [Reply to message](https://docs.agentmail.to/api-reference/inboxes/messages/reply) |

The [harness contract](HARNESS.md) defines the available tools. Use local action recording for generated outbound email actions. Webhook registration is backend integration work; no webhook-management UI is required.

## Local replay

A replay script reads a saved synthetic webhook event and sends an HTTP POST to your local receiving endpoint. Sending the same event again lets you exercise duplicate delivery; changing the input lets you test other cases without sending another email.

Create the payloads and script yourself using the [documented webhook contract](https://docs.agentmail.to/webhooks-overview). Exercise the same receiving, validation, and routing path used by live events, and document how local test signatures are generated and verified.

Local replay needs no public tunnel and is sufficient to demonstrate the flow. Live AgentMail HTTP deliveries require a reachable URL. Build the registration path, but a live public endpoint is not required for the trial.

Your application stores agent configuration separately from AgentMail webhook settings.
