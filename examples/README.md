# Examples

Two Blueprints for a fictional lighting manufacturer, Lumen Fixtures. Every file is a document as described in the top-level README.

* `support/` is the Support team's Blueprint: customers, onboardings, tickets, and the people who handle them.
* `contracts/` is the Legal team's Blueprint: parties, agreements, and clauses.

Support `uses` Contracts, so a ticket can point at the order form it falls under. The two Blueprints never merge. A Mapping in `support/mappings/` says which Support customers and Contracts parties are the same company by matching CRM ids, and one customer without a CRM id on the Contracts side is joined by a hand-written `same-as`.

Things to look for:

* `support/shapes/Escalation.md` extends Ticket, adds a field and a connection, and tightens `owner` to one.
* `support/tickets/Ticket 4411.md` has typed connections in frontmatter and an untyped `related` link in its body.
* `contracts/agreements/OF-2026-031.md` is `part-of` an MSA, and the MSA's `contains` list is never written anywhere. It is derived.
* `support/index.md` and `support/log.md` are the two reserved file names.
