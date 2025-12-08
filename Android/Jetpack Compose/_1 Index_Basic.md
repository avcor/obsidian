### **✔ Composition vs Recomposition**
- [[Declarative(Compose) vs Imperative(XML) UI]]
- [[Composition|Composition and recomposition]]
- [[Compose Rules]]
- Stability & identity
- How keys work in LazyColumn
- [[remember|Why `remember` is tied to composition]]
### **✔ Layout System**
- [[How compose measure and lay out children]]
- [[Intrinsic measurement]]
- [[How compose measure and lay out children]]
- [[Subcompose Layout]]
### **✔ State & Snapshot System**
- rememberSaveable, mutableStateOf, derivedStateOf
- State, State hoisting
- `SnapshotState` internals
-  Snapshot system & snapshot flow
- Snapshot reads/writes
- How Compose detects changes
- `derivedStateOf` and its role in optimization
- Why some changes recompose parent/children
- Threading rules of snapshot state

### **✔ Side-effect APIs (Must master for interviews)**
*Note - These are the heading according to precedence of mostly used side effects*
- [[launchedEffect]]
-  [[rememberCoroutineScope]]
- [[disposableEffect]]
- [[produceState]]
- [[sideEffect]]
- [[rememberUpdateState]]
- [[snapshotFlow]]
Not a side effect but it is important  - [[derievedStateOf]]