**Composition** is the description of UI build by executing the composable function. 
Tree structure representing UI hierarchy 

## How it is built 
when you executes the root composable (`setContent`)
- **Initial Execution** - Compose calls top level  composable
- **Child calls** - If it contains child, it records the 
	- calls
	- arguments
	- relative position in the tree. 
	- local remember values (`remember`)
- **Recording** - Compose records this execution in data structure known as Composition tree. What I remember android stores in a flat array but treat them as tree logically.
- **Display** - The above tree which is executed is used render pixels on the screen. 

## Composition vs Recomposition 
Composition is [[#How it is built|initial run]]
**Recomposition** - re-executing only composable functions whose input have changed 

**The logic**
- Compose tracks every state it read
- If state is changed, compose look up all the node that it reads that specific state
- It then re-render only those specific composable 
- If composable input is not changed and it is a skippable compose. Compose will skip its execution and reuse the value form previous composition 
- If composable input has changed, compose restart its execution to run logic again

***Recomposition is synchronous with current time, but effects (`LaunchedEffect`) are scheduled on coroutines***




