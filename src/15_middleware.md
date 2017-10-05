# Time Travelling!

---

.inline_block[
```javascript
snapshotDisposer = onSnapshot(targetStore, todos => {
    self.history.push(snapshot)
    self.undoIdx++
})
```
]

---

.inline_block[
```javascript
const TimeTraveller = types.model({
        history: types.optional(types.array(types.frozen), []),
        undoIdx: -1,
        targetPath: types.string
    })
    .actions(self => {
        let targetStore, snapshotDisposer

        return {
            afterCreate() {
                targetStore = resolvePath(self, self.targetPath)
                snapshotDisposer = onSnapshot(targetStore, todos => {
                    self.history.push(snapshot)
                    self.undoIdx++
                })
            },
            undo() {
                applySnapshot(targetStore, self.history[--self.undoIdx])
            },
            beforeDestroy() {
                snapshotDisposer()
            }
        }
    })
```
]

???

Frozen type

local state

lifecycle hooks

---

# Demo

---

# But...

.appear[Time travelling with snapshot sucks]

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