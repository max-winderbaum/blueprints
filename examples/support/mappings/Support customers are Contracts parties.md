---
type: Mapping
title: Support customers are Contracts parties
from: { shape: Customer, key: [crm_id] }
to:   { shape: Party,    key: [crm_id] }
---
When a Support Customer and a Contracts Party carry the same CRM id, they are the same company.

This covers every customer signed since the CRM went live in 2025. Older parties have no CRM id in Contracts and are joined by hand with `same-as` on the Customer document, as [[Northwind Traders]] is.
