---
type: Definition
title: Agreement
attributes:
  signed:
    type: date
    one: true
  term_ends:
    type: date
    one: true
  party:
    type: Party
    one: true
    label: Counterparty
  owner:
    type: Person
    one: true
    label: Lumen owner
  part-of:
    type: Agreement
    one: true
    label: Under master agreement
  next:
    type: Agreement
    label: Superseded by
---
~~~instruction-block;kind=voice
Plain English first, then the exact term. Never paraphrase a number or a date.
~~~

# {{key}}

## Summary

~~~instruction-block;max-words=100
What this agreement is for and what it covers. Governing law if it matters.
~~~

## Key dates

~~~instruction-block
Signed, term end, notice deadlines, and any delivery dates with a penalty attached.
~~~
