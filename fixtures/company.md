# Rho billing agent scenario

Rho is the real customer context for this trial: their team wants to create agents for customers without building and hosting each agent service.

Everything below is invented for the exercise. Harbor Operations is a fictional customer workspace, and all contacts use reserved example domains. These are not Rho's operating policies.

## Workflow

An invoice arrives at invoices@harbor.example. The agent should identify the invoice details, prepare a useful reply, and identify who needs to be CC'd in the thread.

For this example, accounts payable handles invoice intake. The purchase owner can confirm the invoice relates to their team's order.

## Routing context

| Role | Address | Responsibility |
| --- | --- | --- |
| Accounts payable | ap@harbor.example | Invoice intake and billing questions |
| Engineering purchase owner | engineering-owner@harbor.example | Engineering purchases; purchase order ENG-204 |
| IT purchase owner | it-owner@harbor.example | IT purchases; purchase order IT-108 |

The available routing context may be incomplete. An annual software license without a purchase order could belong to more than one team. Do not invent an owner or claim payment has been approved.

## Starting instructions

Read the incoming invoice email. Extract the useful invoice information, draft a response, and select relevant CC recipients from the supplied context. Explain uncertainty when the owner or invoice details are unclear. Do not approve or execute payments.

The user should be able to configure the agent's instructions. You decide how to present its output and any proposed action.
