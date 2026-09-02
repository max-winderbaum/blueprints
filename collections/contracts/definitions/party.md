---
type: Definition
title: Party
attributes:
  legal_name:
    type: string
    one: true
  crm_id:
    type: string
    one: true
    label: CRM id, if the party postdates the CRM
  jurisdiction:
    type: string
    one: true
---
# {{key}}

## Legal entity

~~~instruction-block
Full legal name, entity type, jurisdiction, and registered address.
~~~

## Signatory

~~~instruction-block
Name and title of who signs for them.
~~~

## Notices

~~~instruction-block
Where formal notices go, exactly as the agreement says.
~~~
