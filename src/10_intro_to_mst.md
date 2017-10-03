# Demo app!

???

Static demo app, just json

Letś type this

---

# Types

* Describe the shape of the tree
* Runtime checking
* Designtime checking
* Composable & Extensible

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

Connect demo to appstore

---

# Snapshots

<img src="img/git.png" width="50" />

Like a git commit

_Describes the entire state at a specific moment in time_

* .appear[Capture entire state in plain objects]
* .appear[Immutable]
* .appear[Structurally shared]
* .appear[Free]
* .appear[Can be used to create or update instances ].appear[_ Reconciliation_]

???

Free: in perf costs, but also in effor: no need to produce a new state tree

---

# Demo

???

Introduce actions

Tnx local storage for showing changes

---

# Types

* .appear[Enrich data]
* .appear[Actions]
* .appear[Views]
* .appear[Local / private state]
* .appear[Life cycle]

---

# Actions

* .appear[Can change own subtree]
* .appear[Discoverable]
* .appear[Bound]

---

# Demo

???

Add computed fields

Connect observer

Use filteredTodos

---

# Views

* .appear[Derived values]
* .appear[Memoized. Fully reacty. Powered by MobX]
* .appear[`observer` FTW]

