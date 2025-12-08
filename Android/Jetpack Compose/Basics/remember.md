## Why remember is tied to composition 
`remember` store a value in the composition [[#Slot]] for the current composable which survives the re-composition but it is cleared when the composable leaves the composition.

The **Major reason** is also that `remember` lifecycle is also mirror of the composable function 
## Slot
Slot Index is technical concept used by jetpack compose runtime to effectively manage and track the state and data associated with a composable function call. 
When composable function is executed, it allocates some physical space in its internal data structure (**Slot Table**) for the result of function.
Space is allocated purely on order of execution. Specific position is the slot index. 
## How `remember` use [[#Slot]] 
When Compose encounter a `remember{...}` call
- Check current slot index, looks into memory at specified slot  
- If there already a value, it return that existing value. 
- If not then it execute the lambda, store the result in slot and return the result. 

If compose is removed from the tree memory, slot is cleared and state is lost. If you call again same function then it is treated as new composable and remember lambda is ran again . 
Also slot will be reused which was previously associated. 

```kotlin
@Composable
fun ProfileEditor(userId: Int) {
    
    // The key is the userId.
    // If userId changes, remember discards the old 'text' state 
    // and recalculates the initial value (which is "")
    var text by remember(userId) { 
        mutableStateOf("") 
    }
}
```