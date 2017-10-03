## Content in slides notes
We need to sort out if use it, edit it out or split it.

???
Mutable and Immutable are for sure the current opposite paradigms, each one with its pros and its cons.

As developers we always try to find the ultimate solution, and the quest for that solution sometimes make us forget about what we learnt and approach new ways of doing things

So maybe instead of approaching a completely new paradigm, we should look behind, learn from our journey, and see if we can get the best of what we learnt

Mutable data structures are perfect for continuosly-changing values; forms for example are an example of highly-continuosly-changing data structures, that would require lot of new immutable objects to be allocated in memory as we interact with our forms.

On the other hand, Immutable structures are awesome, they allow easy testing and when they only contains serializable data they make easy to de/rehydrate our application state.

---

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

```
enumeration
model
compose
reference
union
optional
literal
maybe
refinement
string
boolean
number
Date
map
array
frozen
identifier
late
undefined
null
```

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

Connect demo to appstore

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

Tnx local storage for showing changes

---

# Actions

* .appear[Can change own subtree]
* .appear[Discoverable]
* .appear[Bound]

---

# Views

* .appear[Derived values]
* .appear[Memoized. Fully reacty. Powered by MobX]
* .appear[`observer` FTW]

---

# Demo

???

Add computed fields

Connect observer

Use filteredTodos


