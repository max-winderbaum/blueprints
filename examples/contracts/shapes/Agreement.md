---
type: Shape
title: Agreement
key: [agreement_id]
connections:
  party:  { shape: Party, one: true, label: Counterparty }
  owner:  { shape: Person, one: true, label: Lumen owner }
  next:   { shape: Agreement, label: Superseded by }
---
# Agreement
## Summary
## Key dates
