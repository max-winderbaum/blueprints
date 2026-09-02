---
type: Definition
title: Person
attributes:
  email:
    type: string
    one: true
  part-of:
    type: Person
    one: true
    label: Reports to
---
# {{key}}

## Role

~~~instruction-block
One or two sentences. What they own and which accounts or areas they cover.
~~~

## Working hours

~~~instruction-block
Days and hours with a time zone, so a colleague knows when a reply is realistic.
~~~
