# Collections

Example Collections for the Collections V0 format.

The format itself is described in one document, [Collections V0](https://comment.io/d/cb92132b51d3b1fbe5a2cbba9b8026162?token=3e203bf1-ec10-463b-ba01-5b4debd7cf0d). Read that first. Everything in this repo is an example of it.

## What is here

`collections/` holds two Collections for a fictional lighting manufacturer, Lumen Fixtures.

* `support/` is the Support team's Collection: people, customers, an onboarding program, tickets, and one escalation.
* `contracts/` is the Legal team's Collection: people, parties, agreements, and clauses.

Support points at Contracts. A ticket's `agreement` names the order form it falls under, and Support's Acme customer is `same-as` Contracts' Acme party. Contracts does not point back.

## Things to look for

* `support/definitions/escalation.md` extends Ticket, adds two attributes, tightens `owner` to one, and adds a template section.
* `support/definitions/ticket.md` uses all three instruction block kinds and a `max-words` target.
* `support/things/ticket/ticket-4411.md` has typed connections in frontmatter and an untyped `related` link in its body.
* `support/things/ticket/ticket-4413.md` is `status: draft`, written by an agent and not yet confirmed.
* `contracts/things/agreement/agreement-OF-2026-031.md` is `part-of` an MSA. The MSA's `contains` list is never written. It is derived.
* Every Thing is filed as `type-key.md` inside a folder named after its type.

## One thing the examples decided

The format reserves `status` for `draft` or `confirmed`. The Ticket definition wanted its own status of open, waiting, or closed. Following the format's rule that the reserved word wins, Ticket calls its own attribute `state`.
