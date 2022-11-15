---
layout: page
title: PostgreSQL Guide
permalink: /guides/postgresql
exclude_from_header: true
---

### Database Design
---
#### **> How can I restrict the possible values for a column?**
You have two options:
1. A `CHECK CONSTRAINT`:
```
ALTER TABLE distributors 
   ADD CONSTRAINT check_types 
   CHECK (element_type = 'lesson' OR element_type = 'quiz');
```
3. A `ENUM`:
```
CREATE TYPE element_type AS ENUM ('lesson', 'quiz');
```
See: \
[In Postgres, how do you restrict possible values for a particular column?](https://stackoverflow.com/questions/7250939/in-postgres-how-do-you-restrict-possible-values-for-a-particular-column)

- - -
