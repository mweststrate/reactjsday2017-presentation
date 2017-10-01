# Introduction to MST (10 min)

How to declare a model using untyped API (e.g. LoginPage with user & pwd fields)
LoginPage.create will produce an observable object with the given defaults
Show that a snapshot could be provided to restore an instance state (either applyState/.create)
Make the audience realize that we could have time travel based on that
A store is snapshot data + model (later we’ll call it type) structure.

---

## Content in slides notes
We need to sort out if use it, edit it out or split it.

???
Mutable and Immutable are for sure the current opposite paradigms, each one with its pros and its cons.

As developers we always try to find the ultimate solution, and the quest for that solution sometimes make us forget about what we learnt and approach new ways of doing things

So maybe instead of approaching a completely new paradigm, we should look behind, learn from our journey, and see if we can get the best of what we learnt

Mutable data structures are perfect for continuosly-changing values; forms for example are an example of highly-continuosly-changing data structures, that would require lot of new immutable objects to be allocated in memory as we interact with our forms.

On the other hand, Immutable structures are awesome, they allow easy testing and when they only contains serializable data they make easy to de/rehydrate our application state.
