---
type: Shape
title: Escalation
extends: Ticket
connections:
  owner:        { shape: Person, one: true }
  escalated-to: { shape: Person, one: true }
---
# Escalation
## What happened
## What we did
## Why it was escalated
## Customer impact
