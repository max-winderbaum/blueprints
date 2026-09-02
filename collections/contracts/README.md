# Contracts

Every agreement Lumen Fixtures has signed, the parties to it, and the clauses inside it that other teams need to find.

Owner: Marcus Bell, Commercial Counsel.

This Collection does not know about tickets or onboardings. Other Collections point at our agreements. We do not point back.

## Kinds of Thing

* Person, keyed by handle.
* Party, a counterparty, keyed by a short slug of its legal name.
* Agreement, a signed contract, keyed by agreement id. Order forms are Agreements that are `part-of` a master agreement.
* Clause, one section of an agreement, keyed by agreement id and section number.
