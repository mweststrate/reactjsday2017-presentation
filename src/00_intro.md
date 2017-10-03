<img src="img/mobx2.png" height="80px" />
<img src="img/logo.png" style="height:80px"/>
## Mutable or Immutable? Why not both!

ReactJS Day Verona 2017

Mattia Manzati - @mattiamanzati

Michel Weststrate - @mweststrate
<br/><br/>

<img src="img/mendix-logo.png" height="60px" /><br/>

---

# How to do state management in React?

.inline_block[

1. .appear[`setState`] .appear[<br/>_Mèh... _].appear[_ said Michele_].appear[_ maybe_]
2. .appear[`Redux`] .appear[<br/>_I guess you get paid by the hour_]
3. .appear[`MobX`] .appear[<br/>_Stop the whitchcraft, heritic!_]
]

.appear[
<i class="em em-astonished"></i>]

---

## Comparing the opposite patterns

.appear[
    `redux === immutable`
]
.appear[
    `mobx === mutable`
]

---


## Redux

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

???

In Redux the reducer could be considered the core concept of data modeling, and that's predictable.
Since we are dealing with immutable data, we could not change an instance, so the focus of our code will
always be the data transformation rather than it's shape.
Due to that, our data shape is kinda lost in all of that code.

---

## Redux

```javascript
const TOGGLE_TODO = 'todo/TOGGLE_TODO'
export function toggleTodo(){
    return { type: TOGGLE_TODO }
}
```

???

And while we are at it, we could note that reducer and actions are'nt colocated, and that IMHO could potentially make our code less readable.

---

## MobX

```javascript
class Todo {
    @observable name = ""
    @observable done = false

    @action toggle(){
        this.done != this.done
    }
}
```

???

Most of the people using MobX up to now used ES6 classes up to now, and that's nice. It lets you write clean code that express both data shape and actions in the same place making it highly readable.

---

### MobX
.appear[Pros: Data shape is clear]

### Redux
.appear[Cons: Data shape is kinda lost]

---

## Data Rehydration

```javascript
const serverData = {
    name: "Attend React Alicante",
    done: true
}
```

---

### Redux

```javascript
const newState = todoReducer(serverData, toggleTodo())
// newState.done === false
```

???

Since Redux uses immutable objects, they won't contain any application business logic like actions, computeds, etc...
So it is really easy to rehydrate data onto our store, you just need to pass it onto your reducer.
---

### MobX

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

???

Unfortunately, MobX uses classes, so it won't accept our server data, we need to define a property and a method to manage de/serialization.

---
### MobX
.appear[Cons: Use classes, internal state, local actions, strong typing, reactivity. But hard de/serialization]

### Redux
.appear[Pros: Use plain objects, external state, no need for de/serialization]

---

## Redux state snapshots are awesome!
- Allow time travel
- Make testing easier
- Better dev tools

---

## What if we could get them for free?
.appear[We need to know the data shape]

.appear[We need de/serialization fn() for each shape]



---

`redux || mobx`

.appear[`true`]

---
