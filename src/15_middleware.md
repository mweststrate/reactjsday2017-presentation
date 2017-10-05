---

class: fullscreenw

<img src="img/opera2.jpg" />

---

# Time Travelling!

<i class="em em-clock8"></i>

---

.inline_block[
```javascript
import { onSnapshot, applySnapshot } from "mobx-state-tree"

const store = SomeModel.create()

const states = []

onSnapshot(store, snapshot => {
    states.push(snapshot)
})

function undo() {
    applySnapshot(store, states.pop())
}
```
]

---

# Demo

???

add time traveller

---

.inline_block[
.appear[
```javascript
const TimeTraveller = types.model({
        history: types.optional(types.array(types.frozen), []),
        undoIdx: -1,
        targetPath: types.string
    })
```
]
.appear[
```javascript
    .actions(self => {
        let targetStore, snapshotDisposer
```
].appear[
```javascript

        return {
            afterCreate() {
                targetStore = resolvePath(self, self.targetPath)
                snapshotDisposer = onSnapshot(targetStore, todos => {
                    self.history.push(snapshot)
                    self.undoIdx++
                })
            },
```
]
.appear[
```javascript
            undo() {
                applySnapshot(targetStore, self.history[--self.undoIdx])
            },
```
]
.appear[
```javascript
            beforeDestroy() {
                snapshotDisposer()
            }
        }
    })
```
]
]

???

Frozen type

local state

lifecycle hooks

---

# Time travelling !== Undo / Redo

<i class="em em-expressionless"></i>


---

# Demo

???

Add timeout stuff

---

# Real undo / redo

.inline_block[
1. .appear[Record patches and inverse apply them].appear[<br/><img src="img/git.png" width="50" />_Like git revert_<br/><br/>]
1. .appear[Record start state, rewind, replay all non-failing actions].appear[<br/><img src="img/git.png" width="50" />_Like git rebase_]
]

---

# Demo

???

Add undo / redo manager

---

# Patches

<img src="img/git.png" width="50" />

Like a git patch

_Describes the modifications from one commit to the next_

.inline_block[
* .appear[Monitor fine grained changes]
* .appear[RFC-6902]
* .appear[Transmission ready]
]

---

.inline_block[
```javascript
// ... like Time Traveller
afterCreate() {
    const undoRedoMiddleware = createActionTrackingMiddleware({
        onStart: call => recordPatches(call.tree),
        onResume: (call, recorder) => recorder.resume(),
        onSuspend: (call, recorder) => recorder.stop(),
        onSuccess: (call, recorder) => {
            self.history.push({
                patches: recorder.patches,
                inversePatches: recorder.inversePatches
            })
        },
        onFail: (call, recorder) => recorder.undo()
    })

    addMiddleware(undoRedoMiddleware, targetStore)
}
```
]

---

.inline_block[
```javascript
function undo() {
    applyPatch(targetStore, self.history[--self.undoIdx].inversePatches)
}
```
]