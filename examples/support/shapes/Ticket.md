---
type: Shape
title: Ticket
key: [ticket_id]
connections:
  customer:  { shape: Customer, one: true }
  part-of:   { shape: Onboarding, one: true }
  next:      { shape: Ticket, label: Follow-up }
  owner:     { shape: Person }
  agreement: { shape: Order form, one: true, label: Falls under }
---
# Ticket
## What happened
## What we did
