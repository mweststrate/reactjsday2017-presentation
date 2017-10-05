<img src="img/mobx2.png" height="80px" />
<img src="img/logo.png" style="height:80px"/>
## Mutable or Immutable? Both!

ReactJS Day Verona 2017

Mattia Manzati - @mattiamanzati

Michel Weststrate - @mweststrate
<br/><br/>

<img src="img/mendix-logo.png" height="60px" /><br/>

---

# How to do state management in React?

.inline_block[

1. .appear[`setState`] .appear[<br/>_Mèh... _].appear[_ said Michele_].appear[_ maybe_]
2. .appear[`Redux`] .appear[<br/>_You get paid per hour?_]
3. .appear[`MobX`] .appear[<br/>_Stop the whitchcraft, heritic!_]
]

.appear[
<i class="em em-astonished"></i>]

---

# Comparing the opposite patterns

.appear[
    `redux === immutable`
]
.appear[
    `mobx === mutable`
]

???

Mutable and Immutable are for sure the current opposite paradigms, each one with its pros and its cons.

As developers we always try to find the ultimate solution, and the quest for that solution sometimes make us forget about what we learnt and approach new ways of doing things

So maybe instead of approaching a completely new paradigm, we should look behind, learn from our journey, and see if we can get the best of what we learnt

Mutable data structures are perfect for continuosly-changing values; forms for example are an example of highly-continuosly-changing data structures, that would require lot of new immutable objects to be allocated in memory as we interact with our forms.

On the other hand, Immutable structures are awesome, they allow easy testing and when they only contains serializable data they make easy to de/rehydrate our application state.

---


# Redux

.inline_block[
```javascript
const initialState = {name: "", done: false}
function todoReducer(state = initialState, action){
    if(!action) return state

    switch(action.type){
        case TOGGLE_TODO:
            return ({...state, done: !state.done})
        default:
            return state
    }
}
```
]

???

In Redux the reducer could be considered the core concept of data modeling, and that's predictable.
Since we are dealing with immutable data, we could not change an instance, so the focus of our code will
always be the data transformation rather than it's shape.
Due to that, our data shape is kinda lost in all of that code.

---

# Redux

.inline_block[
```javascript
const TOGGLE_TODO = 'todo/TOGGLE_TODO'
export function toggleTodo(){
    return { type: TOGGLE_TODO }
}
```
]

???

And while we are at it, we could note that reducer and actions are'nt colocated, and that IMHO could potentially make our code less readable.

---

# MobX

.inline_block[
```javascript
class Todo {
    @observable name = ""
    @observable done = false

    @action toggle(){
        this.done != this.done
    }
}
```
]

???

Most of the people using MobX up to now used ES6 classes up to now, and that's nice. It lets you write clean code that express both data shape and actions in the same place making it highly readable.

---

`MobX`

Data shape is explicit

`Redux`

Data shape is implicit

---

# Data Rehydration

.inline_block[
```javascript
const serverData = {
    name: "Visit the opera!",
    done: true
}
```
]

---

# Redux

.inline_block[
```javascript
const newState = todoReducer(serverData, toggleTodo())
// newState.done === false
```
]

???

Since Redux uses immutable objects, they won't contain any application business logic like actions, computeds, etc...
So it is really easy to rehydrate data onto our store, you just need to pass it onto your reducer.
---

# MobX

.inline_block[
```javascript
class Todo {
    // ...
    @computed get snapshot(){
        return {
            name: this.name,
            done: this.done
        }
    }

    @action applySnapshot(snapshot){
        this.name = snapshot.name
        this.done = snapshot.done
    }
}
```
]

???

Unfortunately, MobX uses classes, so it won't accept our server data, we need to define a property and a method to manage de/serialization.

---
`MobX`

(Usually) classes. Unlimited data shape. De/serialization is hard

`Redux`

Plain objects. Tree structure only. Serialization is done in actions

---

# Redux state snapshots are awesome!

.inline_block[
- Allow time travel
- Make testing easier
- Better dev tools
]

---

# What if we could get them for free?

.appear[Declare data shape]

.appear[De/serialization can be derived]

---

`redux || mobx`

.appear[`true`]

---
