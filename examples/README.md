# Examples

Two Blueprints for a fictional lighting manufacturer, Lumen Fixtures. Every file is a document as described in the top-level README.

* `support/` is the Support team's Blueprint: customers, onboardings, tickets, and the people who handle them.
* `contracts/` is the Legal team's Blueprint: parties, agreements, and clauses.

Each folder has one Blueprint file at its root, `Support.md` and `Contracts.md`, which declares every Shape and holds each Shape's template. Every other file is a document, filed in a top-level folder named after its Shape. `support/other/` holds one document with no Shape.

Support `uses` Contracts, so a ticket can point at the order form it falls under. The two Blueprints never merge. The two Acme documents are joined by a `same-as` on the Support side, and so are the two Northwind documents.

Things to look for:

* `Escalation` in `support/Support.md` extends Ticket, adds a property and a connection, and tightens `owner` to one.
* `support/Ticket/Ticket 4411.md` has typed connections in frontmatter and an untyped `related` link in its body.
* `contracts/Order form/OF-2026-031.md` is `part-of` an MSA, and the MSA's `contains` list is never written anywhere. It is derived.
* `index.md` and `log.md` are the two reserved file names.
