---
type: Blueprint
title: Contracts
owner: [[Marcus Bell]]
shapes:
  Person:
    key: [email]
    properties: [email]
  Party:
    key: [legal_name]
    properties: [legal_name, crm_id, jurisdiction]
  Agreement:
    key: [agreement_id]
    properties: [agreement_id, signed, term_ends]
    connections:
      party: { shape: Party, one: true, label: Counterparty }
      owner: { shape: Person, one: true, label: Lumen owner }
      next:  { shape: Agreement, label: Superseded by }
  Order form:
    extends: Agreement
    connections:
      part-of: { shape: Agreement, one: true, label: Under MSA }
  Clause:
    properties: [section]
    connections:
      part-of: { shape: Agreement, one: true }
---
Every agreement Lumen Fixtures has signed, the parties to it, and the clauses inside it that other teams need to find.

This Blueprint does not know about tickets or onboardings. Other Blueprints point at our agreements. We do not point back.

# Person
## Role

# Party
## Legal entity
## Signatory
## Notices

# Agreement
## Summary
## Key dates

# Order form
## Summary
## Key dates
## What was ordered

# Clause
## Plain English
## Exact wording
