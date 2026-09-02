---
type: Definition
title: Ticket
attributes:
  opened:
    type: date
    one: true
  state:
    type: string
    one: true
    values: [open, waiting, closed]
  severity:
    type: string
    one: true
    values: [low, normal, high]
  channel:
    type: string
    one: true
    label: How it reached us
  tags:
    type: string
  customer:
    type: Customer
    one: true
  reporter:
    type: string
    label: Who at the customer reported it
  owner:
    type: Person
    label: Handling
  agreement:
    type: contracts/Agreement
    one: true
    label: Falls under
  part-of:
    type: Onboarding
    one: true
  next:
    type: Ticket
    label: Follow-up
---
~~~instruction-block;kind=voice
Plain sentences. A date on every action. Quote the customer where you can.
~~~

# Ticket {{key}}

~~~instruction-block;kind=document
One reported problem from one customer. Open a new ticket for a new problem, even from the same customer on the same day. If this ticket leads to another, link it with next rather than reopening this one.
~~~

## What happened

~~~instruction-block;max-words=150
Say what the customer saw, when, and who told us. Do not diagnose here.
~~~

## What we did

~~~instruction-block
One line per action, newest last, each with a date. Include what we told the customer and when. If a clause in the agreement sets a deadline, link the clause and name the date it implies.
~~~
