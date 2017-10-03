# Time Travelling!

---

# Demo

---

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

???

Frozen type

local state

lifecycle hooks

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

# Middleware


<img src="img/git.png" width="50" />

Like git hooks

_pre- / post process specific commands_

* .appear[Listen to specific action or all actions in subtree]
* .appear[First class support for asynchronous processes]
* .appear[`addMiddleware(store, handler)`]
* .appear[`handler: (call: ICall, next: (call) => any) => any`]



---

# Patches

RFC-6902
Transmission ready

<img src="img/git.png" width="50" />

Like a git patch

_Describes the modifications from one commit to the next_

Fine grained


---

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
},
undo() {
    applyPatch(targetStore, self.history[--self.undoIdx].inversePatches)
}
```