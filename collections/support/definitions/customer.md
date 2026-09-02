---
type: Definition
title: Customer
attributes:
  plan:
    type: string
    one: true
    values: [Standard, Enterprise]
  owner:
    type: Person
    one: true
    label: Account owner
---
# {{key}}

~~~instruction-block;kind=document
One company we support. The key is their CRM id. If the same company appears in Contracts, link it with same-as rather than copying anything across.
~~~

## Who they are

~~~instruction-block;max-words=80
Industry, size, location, and what they use our fixtures for.
~~~

## What they buy from us

~~~instruction-block
Product lines and rough volumes. Link the agreement rather than quoting terms.
~~~

## Watch out for

~~~instruction-block
Anything a new support engineer must know before replying. Named contacts, response expectations, contract clauses that bite.
~~~
