## Stable Meaning
> Stable means compose can trust that if reference does not change then content did not change.
> Compose avoids structural (deep) equality because it is expensive. Instead it relies on referential equality + stability guarantees.   
> Its about predictability + observability  
## Types of stability 
### Stable
- Primitive type Int, Boolean - always stable 
- String (Immutable)
- Function types (Lambdas) 
- Classes where all types are immutable (val) and stable 
- Data Class - Not automatically stable unless proved
	- It does not know if fields change internally 
	- It does not track deep equality automatically
### Stable (but Mutable)
A type that can be mutable but notifies the compose when it changes 
- `MutableState` - `mutableStateOf()` is tracked by compose runtime.
### Unstable Types
This types can force compose to recompose because compiler cannot trust them. 
- Interfaces: The compiler does not know underlying implementation it could be mutable class.
- List, Set, Map are just interfaces . List could be `ArrayList`
	- Solutions
		- Use `ImmutableList`
		- Wrap list in data class with `@Immutable

## How stability works
It is a mechanism of compose that allows to skip the composition of a composable function during recomposition. 
When it can be skipped - all of its parameter are of [[Stable#Types of stability#Stable|Stable]] type  
- When compose run for first time compose records its input
- During the recomposition compose compares the new input with the cached inputs.
	- If all the stable inputs are equal to previous input then composition is skipped 
	- If any stable inputs are not equal or has unstable parameters the function is executed 

## Why lambda causes recomposition 
- Lambda function are skippable if all the parameter are stable by using lambda memoization. 
### When does it becomes unstable 
- Capturing Unstable data types such as list, map
- Passing method reference `viewmodel::myFunc` bypasses compiler memoization 
### Fix
You can use remember function 
```kotlin
val onClick = remember(state) { { doSomething(state) } }
```


