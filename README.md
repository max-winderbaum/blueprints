# Composable Ontologies V0

An ontology is a folder of Markdown files. This document says what goes in the files.

## Terminology

**Blueprint.** A whole ontology. One folder, one owner, one domain. Support is a Blueprint. Contracts is a Blueprint.

**Shape.** One kind of thing in a Blueprint. A Ticket is a Shape. A Customer is a Shape. A Shape says what a document of that kind looks like and what it may connect to.

**Document.** A Markdown file. Ticket 4411 is a document. A document usually follows a Shape, but does not have to.

**Connection.** A named link from one document to another. A ticket's `customer` is a connection.

## Two kinds of file

A Blueprint folder holds exactly two kinds of file.

1. **The Blueprint file.** One per folder, at the root. It declares every Shape and how they relate.
2. **Documents.** Every other Markdown file. They can live anywhere in the folder and reference each other.

Two file names are reserved and are neither: `index.md` for listings and `log.md` for history. They may appear in any folder.

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

* `type` names the Shape. A document with no `type` follows no Shape and may still connect to anything.
* A connection is a field whose value is one wikilink or a list of wikilinks.
* Any other field is a property, a plain value such as `ticket_id` above.
* A link in the body is a connection too. Its name is `related`.
* Unknown fields are kept. Nothing is ever thrown away.

## The Blueprint file

The Blueprint file's frontmatter names the Blueprint and declares its Shapes. Its body holds one heading per Shape, and the text under each heading is the template a new document of that Shape starts from.

```
---
type: Blueprint
title: Support
owner: [[Dana]]
uses:
  - [[Contracts]]
shapes:
  Customer:
    key: [crm_id]
    properties: [crm_id, plan]
    connections:
      owner: { shape: Person, one: true }
  Ticket:
    key: [ticket_id]
    properties: [ticket_id, opened, status]
    connections:
      customer: { shape: Customer, one: true }
      part-of:  { shape: Onboarding, one: true }
      next:     { shape: Ticket, label: Follow-up }
  Escalation:
    extends: Ticket
    properties: [severity]
    connections:
      escalated-to: { shape: Person, one: true }
---
Everything the support team tracks.

# Customer
## Who they are
## What they buy from us

# Ticket
## What happened
## What we did

# Escalation
## What happened
## What we did
## Why it was escalated
```

Rules:

* Each key under `shapes` is a Shape's name. Documents use it as their `type`.
* `properties` lists the plain fields a document of this Shape carries.
* `connections` lists each connection name, the Shape it points at, and whether there can be only one. Everything is many unless `one: true` is set.
* `key` names the properties that identify a document. Two documents of the same Shape with the same key are the same thing.
* `extends` names a parent Shape. The child gets the parent's properties, connections, and template, and may add to them or tighten them. It may never remove or loosen them.
* A connection may carry a `label` for display. The field name in documents is always the connection name itself.
* `uses` names other Blueprints whose Shapes this one may connect to.

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

## Where documents live

Documents may live anywhere in the Blueprint folder. Frontmatter decides what a document is, never its path.

The strong suggestion is one top-level folder per Shape, named exactly as the Shape, plus `other/` for documents with no `type`.

```
support/
  Support.md
  Customer/
    Acme Robotics.md
  Ticket/
    Ticket 4411.md
  Escalation/
    Ticket 4418.md
  other/
    Team offsite notes.md
```

A document in a folder that does not match its `type` is a warning, not an error.

## Saying two things are the same

Inside one Blueprint, two documents of one Shape with the same key are the same thing. If you find two, merge them into one file.

Across Blueprints, do not merge. Support's Acme and Contracts' Acme have different Shapes, different owners, and different lives. They stay separate and are joined with `same-as`.

```
---
type: Customer
crm_id: CRM-10422
same-as: [[Acme Robotics Inc]]
---
```

How a `same-as` gets written is outside this standard. A person can type it. A tool can generate it from matching CRM ids or anything else. The result is always a `same-as` line in a file.

## Composing Blueprints

Two Blueprints compose by one Blueprint naming the other in `uses` and then connecting to its Shapes or asserting `same-as` onto its documents. Neither Blueprint changes. A Shape that `extends` a Shape from another Blueprint may only add and tighten, so the result is the same no matter which Blueprint is read first.

## Checking

A checker reads a Blueprint and reports warnings. It never refuses a file. The warnings are:

* a `type` that names no Shape
* a connection the Shape did not declare
* a connection pointing at a document of the wrong Shape
* more than one value on a connection marked `one: true`
* two documents of one Shape with the same key
* a property the Shape did not declare
* a link to a document that does not exist
* a connection written on both sides
* a document in a folder that does not match its `type`

A tool may treat any of these as an error if it wants to. The standard does not.

## What is not in V0

* Any way to name a connection other than its built-in or declared name
* Any rule for deciding when two documents are the same
* Any format for a stored graph, index, or cache
* Any required folder layout. The one above is a suggestion.
* Any property types beyond what YAML already has

## Examples

See [`examples/`](examples/) for two Blueprints, Support and Contracts, that compose through `uses` and `same-as`.
