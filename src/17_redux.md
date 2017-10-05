# MST as Redux

.inline_block[
- `state` &rarr; snapshot
- `subscribe` &rarr; `onSnapshot`
- `dispatch` &rarr; `applyAction`
- `connect` &rarr; `observer`
]

---

# MST as Redux

.inline_block[
```javascript
import {asReduxStore}
    from 'mobx-state-tree/middleware/redux'

const reduxStore = asReduxStore(store)
```
]

.appear[<i class="em em-cupid"></i>]

---

# Demo

???

connect devtools