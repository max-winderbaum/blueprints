# Composable Ontologies V0

An ontology is a folder of Markdown files. This document says what goes in the files.

## Terminology

**Blueprint.** A whole ontology. One folder, one owner, one domain. Support is a Blueprint. Contracts is a Blueprint.

**Shape.** One kind of thing inside a Blueprint. A Ticket is a Shape. A Customer is a Shape. Every Shape is a Markdown file that says what a document of that Shape looks like and what it may connect to.

**Document.** A Markdown file that follows a Shape. Ticket 4411 is a document.

**Connection.** A named link from one document to another. A ticket's `customer` is a connection.

## A document

A document is YAML frontmatter followed by a Markdown body. The frontmatter says which Shape it follows and lists its connections. The body is free writing.

```
---
type: Ticket
ticket_id: 4411
customer: [[Acme]]
part-of: [[Q3 onboarding]]
next: [[Ticket 4412]]
---
Acme's welcome kit arrived without the setup card. Send a replacement.
```

Rules:

* `type` names the Shape. It is the only required field.
* A connection is a field whose value is one wikilink or a list of wikilinks.
* Any other field is a plain value, such as `ticket_id` above.
* A link in the body is a connection too. Its name is `related`.
* Unknown fields are kept. Nothing is ever thrown away.

## A Shape

A Shape is a document whose `type` is `Shape`. Its frontmatter declares fields and connections. Its body is the template a new document starts from.

```
---
type: Shape
title: Ticket
key: [ticket_id]
connections:
  customer: { shape: Customer, one: true }
  part-of:  { shape: Onboarding, one: true }
  next:     { shape: Ticket }
---
# Ticket
## What happened
## What we did
```

Rules:

* `title` is the Shape's name. Documents use it as their `type`.
* `key` names the fields that identify a document. Two documents of the same Shape with the same key are the same thing.
* `connections` lists each connection name, the Shape it points at, and whether there can be only one. Everything is many unless `one: true` is set.
* `extends` names a parent Shape. The child gets the parent's fields, connections, and template, and may add to them or tighten them. It may never remove or loosen them.
* A connection may carry a `label` for display. The field name in documents is always the connection name itself.

## Four built-in connections

Every Blueprint gets these four for free. They are the only connections with fixed meaning.

| Name      | Reverse    | Meaning                                                         |
| --------- | ---------- | --------------------------------------------------------------- |
| `part-of` | `contains` | This document belongs inside that one. Chains form a hierarchy. |
| `next`    | `previous` | That document comes after this one. Chains form a sequence.     |
| `same-as` | `same-as`  | These two documents are the same thing.                         |
| `related` | `related`  | These two documents have something to do with each other.       |

Use the built-in name directly. A process that wants "do next" writes `next` in the file and puts "Do next" in the Shape's `label`.

## Where a connection is written

Each connection is written once, on one side. The other side is worked out by reading.

* `part-of` is written on the inner document.
* `next` is written on the earlier document.
* `same-as` is written on either one.
* `related` is written wherever the link appears.
* A Shape's own connection is written on the document whose Shape declares it.

Nothing in the standard says how a reader stores or caches the worked-out reverse links.

## A Blueprint

A Blueprint is a folder. At its root is a document whose `type` is `Blueprint`.

```
---
type: Blueprint
title: Support
owner: [[Dana]]
uses:
  - [[Contracts]]
---
Everything the support team tracks.
```

Rules:

* Every `.md` file in the folder is a document of this Blueprint, except `index.md` and `log.md`, which are reserved for listings and history.
* Shapes are documents in the folder like any other.
* `uses` names other Blueprints whose Shapes this one may connect to.

## Saying two things are the same

Inside one Blueprint, two files about the same thing should be merged into one file. Across Blueprints, they should not. Support's Acme and Contracts' Acme have different Shapes, different owners, and different lives. They stay separate and are joined with `same-as`.

A `same-as` connection can be written by hand, or produced by a rule. A rule lives in a document of the built-in Shape `Mapping`.

```
---
type: Mapping
title: Support customers are Contracts parties
from: { shape: Customer, key: [crm_id] }
to:   { shape: Party,    key: [crm_id] }
---
When the CRM ids match, it is the same company.
```

A Mapping with matching keys is enough for a reader to treat the two documents as one. How anything else decides two documents are the same is outside this standard. Whatever decides, the result is a `same-as` connection written into a file.

## Composing Blueprints

Two Blueprints compose by one Blueprint naming the other in `uses` and then connecting to its Shapes or mapping onto them. Neither Blueprint changes. A Shape that `extends` a Shape from another Blueprint may only add and tighten, so the result is the same no matter which Blueprint is read first.

## Checking

A checker reads a Blueprint and reports warnings. It never refuses a file. The warnings are:

* a `type` that names no Shape
* a connection the Shape did not declare
* a connection pointing at a document of the wrong Shape
* more than one value on a connection marked `one: true`
* two documents of one Shape with the same key
* a link to a document that does not exist
* a connection written on both sides

A tool may treat any of these as an error if it wants to. The standard does not.

## What is not in V0

* Any way to name a connection other than its built-in or declared name
* Any rule for deciding sameness beyond matching keys
* Any format for a stored graph, index, or cache
* Any required folder layout inside a Blueprint
* Any field types beyond what YAML already has

## Examples

See [`examples/`](examples/) for two Blueprints, Support and Contracts, that compose through a Mapping.
