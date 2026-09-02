---
type: Blueprint
title: Support
owner: [[Dana Okafor]]
uses:
  - [[Contracts]]
shapes:
  Person:
    key: [email]
    properties: [email]
    connections:
      part-of: { shape: Person, one: true, label: Reports to }
  Customer:
    key: [crm_id]
    properties: [crm_id, plan]
    connections:
      owner: { shape: Person, one: true, label: Account owner }
  Program:
    properties: [starts, ends]
    connections:
      owner: { shape: Person, one: true }
  Onboarding:
    connections:
      customer: { shape: Customer, one: true }
      part-of:  { shape: Program, one: true }
      owner:    { shape: Person, one: true }
  Ticket:
    key: [ticket_id]
    properties: [ticket_id, opened, status]
    connections:
      customer:  { shape: Customer, one: true }
      part-of:   { shape: Onboarding, one: true }
      next:      { shape: Ticket, label: Follow-up }
      owner:     { shape: Person }
      agreement: { shape: Order form, one: true, label: Falls under }
  Escalation:
    extends: Ticket
    properties: [severity]
    connections:
      owner:        { shape: Person, one: true }
      escalated-to: { shape: Person, one: true }
---
Everything the Lumen Fixtures support team tracks: who our customers are, how their onboarding is going, and every ticket they raise.

Tickets may point at the agreement they fall under, which lives in the [[Contracts]] Blueprint. We never copy contract terms into a ticket. We link to them.

# Person
## Role
## Working hours

# Customer
## Who they are
## What they buy from us
## Watch out for

# Program
## Goal
## Dates

# Onboarding
## Milestones
## Blockers

# Ticket
## What happened
## What we did

# Escalation
## What happened
## What we did
## Why it was escalated
## Customer impact
