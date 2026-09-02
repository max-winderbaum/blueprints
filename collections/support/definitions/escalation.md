---
type: Definition
title: Escalation
extends: Ticket
attributes:
  severity:
    type: string
    one: true
    values: [high]
  owner:
    type: Person
    one: true
  escalated-to:
    type: Person
    one: true
  decision-by:
    type: date
    one: true
    label: Decision needed by
---
# Escalation {{key}}

## Why it was escalated

~~~instruction-block
Name the thing the owner cannot decide alone. Usually money, a contract date, or a customer relationship.
~~~

## Customer impact

~~~instruction-block;max-words=60
What the customer loses if nothing is decided by the date above.
~~~
