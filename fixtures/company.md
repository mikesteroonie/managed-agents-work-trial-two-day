# Example agent configurations

These examples illustrate how different customer needs can be expressed as agent configuration.

The following examples are fictional configurations for Harbor Operations, an invented customer workspace. All contacts use reserved example domains. These are not real customer policies or data.

Use these to exercise one shared managed-agent product. Instructions and context should be configuration, not branches in application code. Customers should be able to provide other instructions for the same harness and toolset.

## Example 1: Billing coordination

Inbox: invoices@harbor.example.

Suggested instructions: Read the incoming invoice, summarize the useful details, and prepare a response that includes appropriate contacts from the supplied context. Explain uncertainty when the purchase owner is unclear. Do not claim payment has been approved or executed.

Example context:

| Role | Address | Responsibility |
| --- | --- | --- |
| Accounts payable | ap@harbor.example | Invoice intake and billing questions |
| Engineering purchase owner | engineering-owner@harbor.example | Engineering purchases; purchase order ENG-204 |
| IT purchase owner | it-owner@harbor.example | IT purchases; purchase order IT-108 |

Try the invoice, missing-owner, and corrected-invoice emails. Their results may include invoice details and proposed recipients.

## Example 2: Support coordination

Inbox: support@harbor.example.

Suggested instructions: Read the customer issue, summarize it, and prepare an acknowledgement. Identify a relevant engineer from the supplied context if possible. Ask for missing details and do not claim the issue is fixed. Record any proposed email action through the supplied tool.

Example context:

| Area | Address | Responsibility |
| --- | --- | --- |
| Integrations | integrations-engineer@harbor.example | Webhook delivery and API integration |
| Dashboard | dashboard-engineer@harbor.example | Console pages, access, and user-interface errors |

Try the webhook support email. Its result may include a problem summary and a proposed engineer to CC.

The two configurations need not produce identical content. The platform should save and display their results and tool activity through the same underlying concepts and execution path.
