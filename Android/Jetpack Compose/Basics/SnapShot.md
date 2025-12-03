## Snapshot 
Immutable view of mutable state objects in a specific point of time 
## Snapshot System 
- It is a mechanism that allows compose to track all changes to `mutable state` and schedule efficient recomposition (UI Updates). 
- System for concurrency control and change observation 
### How it works 
- **Read** - When a composable read a `MutableState` the compose register that read in current global snapshot. *This is how compose know which composable depends on that state variable*
- **Write** - when value is changed of `MutableState` the change is recorded in current active snapshot
### Key Snapshot 
#### Global Snapshot 
The single - present source of truth. All changes merge into this. 
#### Active Snapshot
Snapshot which is currently used by the running code. (often thread local). It ensure that all states access on a given thread is consistent and isolated. 
#### Mutable Snapshot
Used in writing the state. Changes recorded over here can be applied to global or disposed off (abandon) 
#### Read-only Snapshot
Used by `recompositionScope` during rendering. This guarantee that composable reads a consistent, unchanging view during execution. Composition always run in this   
### Flow (The loop)
1. **State Change** - On button click mutable state changes `counter.value`. This happens in [[#Mutable Snapshot]]
2. **Notification** - Mutable snapshot when applied to [[#Global snapshot]], now system knows which state variables changed
3. **Invalidation** - [[#How it works|Read dependencies]], the system identifies the all composable that read a state. These scopes are marked invalid. 
4. **Recomposition** - Compose's `Animataion/Recomposition-Scheduler` wakes up and execute the only invalidated scopes, inside a new [[#Read-only Snapshot]], updating the UI.  

***Note*** - read and write state is associated with [[#Active Snapshot]] . 