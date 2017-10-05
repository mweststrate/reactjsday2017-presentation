# Demo

???

Static demo app, just json

Letś type this

---

# Types

.inline_block[
* Describe the shape of the tree
* Runtime checking
* Designtime checking
* Composable & Extensible
]

---

Split to primitives, collection, higher order types

```
model
map
array

string
literal
boolean
number
Date
reference
frozen
undefined
null

enumeration
compose
union
optional
maybe
refinement
identifier
late
```

---


# Demo

???

Connect demo to app store

---

# Types

* .appear[Enrich data]
* .appear[Actions]
* .appear[Views]
* .appear[Local / private state]
* .appear[Life cycle]

---

# Demo

???

Introduce actions

Connect observer

---

# Actions

.inline_block[
* .appear[Can change own subtree]
* .appear[Discoverable]
* .appear[Bound]
]

---

# Demo

???

Add computed fields


Use filteredTodos

---

# Views

.inline_block[
* .appear[Derived values]
* .appear[Memoized. Fully reacty. Powered by MobX]
* .appear[`observer` FTW]
]

---

# Demo

???

add local storage

---

# Snapshots

<img src="img/git.png" width="50" />

Like a git commit

_Describes the entire state at a specific moment in time_

.inline_block[
* .appear[Immutable]
* .appear[Structurally shared]
* .appear[Free]
* .appear[Can be used to apply changes].appear[<br/>_ Reconciliation_]
]

???

Free: in perf costs, but also in effor: no need to produce a new state tree
