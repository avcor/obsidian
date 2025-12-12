## Stable Means
A type is considered stable if 
- **Immutability** - If the value does not change after construction. Once created, its object state must remain same. 
- **Referential Stability** - If type is primitive (Int, String, Boolean or Immutable collection i.e. `ImmutableList`) then it is stable. For Complex type its underlying fields must be stable 
- **Visible getter / setter** - All public properties must expose stable getters. If a property has custom setter then compose compiler should be able to infer that it will act in a stable way i.e it should guarantee that it will not mutate the object state or change is tracked / observable.
```kotlin 
class UserProfile {
    val name: String = "Alice"
    var age by mutableStateOf(30)
}
```

If compose compiler guarantee these condition by checking the source code or using kotlin features like `val` or `@Immtable` it marks the type stable 
## How stability works
It is a mechanism of compose that allows to skip the composition of a composable function during recomposition. 
When it can be skipped - all of its parameter are of [[Stable - Immutable Annotation#Stable Means|Stable]] type  

- When compose run for first time compose records its input
- During the recomposition compose compares the new input with the cached inputs.
	- If all the stable inputs are equal to previous input then composition is skipped 
	- If any stable inputs are not equal or has unstable parameters the function is executed 

## Why lambda causes recomposition 
lambda functions `onClikc={}` are treated as unstable by compose compiler even if they do not capture external state.  This make a composable **non-skippable** skippable.
When parent recomposes the new instance of lambda often created even though it is same.
Solution 
```kotlin 
val stableCallback = remember {
    { itemId -> /* Do something with itemId */ }
}
MySkippableItem(onClick = stableCallback)
```



