### **✔ Performance**
- Recomposition debugging
- Using `Trace`, Layout inspector
- Stable vs Immutable
- `@Stable`, `@Immutable` annotations
- Avoiding unnecessary object creations
- Skippability
- Using Keys correctly (lazy lists)
- Avoiding lambdas as parameters
- Using `rememberSaveable` with custom savers
- Performance of Lazy Lists & grids
### **✔ Stable / Immutable annotations**
- What makes a type stable
- How skippability works
- Why lambdas cause recomposition
- Why data classes may not be stable
- Best practices for maintaining stability
### **✔ Recomposition Performance**
- Using Recomposition counters
- Why unnecessary objects/lambdas matter
- Passing modifiers efficiently
- Using `remember` with heavy objects
- Avoiding recomposing the entire screen
### **✔ Lazy Layouts Performance**
- Keys
- Item identity
- How LazyColumn measures items
- How to optimize long lists
- Why you should avoid nested lazy lists
### **✔ Custom layout & SubcomposeLayout**
(Companies love this. It shows deep understanding.)
- Intrinsics
- Constraints
- Custom measurement
- SubcomposeLayout use cases
    - Collapsing toolbar
    - Expanding cards
    - Sticky headers
    - Carousels