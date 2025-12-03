### **✔ Composition vs Recomposition**
- [[Declarative(Compose) vs Imperative(XML) UI]]
- [[Composition|Composition and recomposition]]
- [[Compose Rules]]
- Stability & identity
- How keys work in LazyColumn
- [[Remember|Why `remember` is tied to composition]]
### **✔ Layout System**
- How Compose measures and lays out children
- Intrinsic measurements
- Custom Layouts with `Layout {}`
- SubcomposeLayout (very important for performance-heavy components)
- Constraints and alignment lines
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
- `rememberUpdatedState`
- `SideEffect`
- `produceState`
- `snapshotFlow`

Not a side effect but it is important 
[[derievedStateOf]]