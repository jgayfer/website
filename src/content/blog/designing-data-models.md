---
author: James Gayfer
title: Designing data models
description: There's nothing like a good data model, but designing one is easier said than done.
featured: false
postSlug: designing-data-models
pubDatetime: 2024-10-31T12:00:00.000Z
tags:
  - dev
---

There's nothing like a good data model. Well structured data is not only easy to
work with, but can also influence intelligent API design. Getting there however
is easier said than done. Anyone can assert that a data model is "good".
The challenge lies in designing a system that works today, stands up to the
problems of tomorrow, and influences future design decisions for the better.

Most systems rely on some form of persistence. Relational databases are a
popular choice for this, but rows in a database don't always map directly to
domain models. Pulling rows from a database and calling those your domain
models, while easy, can result in an incomplete data model. A row may not be
useful on its own, requiring additional data fetches. An incomplete data model
can also lead to more widespread database access, coupling large swaths of an
application to the persistence layer.

**Incomplete data models lead to incomplete APIs**. Passing IDs around and
returning values that aren't usable alone are a symptom of an incomplete data
model. Additional APIs are needed to combat the lack of information, bloating
the number of services needed. A vicious cycle ensues: **every incomplete
API necessitates another**.

## A bundle of IDs

```rust
struct Membership {
    pub id: i32,
    pub user_id: i32,
    pub team_id: i32,
}
```

Consider the above `Membership` model. We can see it almost certainly represents
a many-to-many relationship between a "user" and a "team". Prior knowledge might
tell us our database has a `teams` and `users` table. We may even know which
application code can fetch these models for us.

However, **identifiers only imply information; they don't have meaning in
themselves**. If we're not able to ascertain where the (presumably) associated
data comes from, our only choice is to go hunting (and hope we get it right).

```rust
struct Membership {
    pub id: i32,
    pub user: User,
    pub team: Team,
}
```

What if instead we provided a reference to the corresponding `User` and `Team`
models? We've moved from implying associations to providing them outright,
lightening the burden of understanding. We've also removed the need for
subsequent data fetches.

The latter `Membership` is certainly more usable, but at what cost?
`Membership`, `Team`, and `User` likely all come from different tables. Our
query is suddenly a lot more involved.

## Managing complexity

In a world of modelling complete associations, there needs to be tradeoffs.
Including the full tree of associated data isn't realistic (or possible) in many
cases. Does a `Team` include a list of associated `Membership` items in the
above example? We'd quickly run into untenable amounts of data.

What parts of the tree should we model? The golden rule is to **do what makes your
life easier**. I've searched for a more prescriptive best practice, but I don't
believe there's a one-size-fits-all solution. Designing the data model _before_
thinking about persistence can be effective, as it forces you to think about how
you want to actually use your models. When in doubt, **if it hurts, don't do
it**.

Building a good data model is hard. It's more work to build up models from data
residing in multiple tables. It's hard to design data models that positively
influence API design. Getting it "right" requires experimentation, and sometimes
it won't pan out. It's okay to throw things away; knowing what doesn't work is
valuable. The goal is for our up front effort to pay off as our thoughtfully
designed data model permeates the rest of the system.
