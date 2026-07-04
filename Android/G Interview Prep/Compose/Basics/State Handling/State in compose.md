Any data that influence what the user sees or can do. It influences the UI. 
## State in compose Ideology 
### View System 
- UI + state + logic often live together 
	- View Model existed, but it was optional and did not enforce stateless UI. The View system still rely implicit state inside views and silent restoration through view hierarchy. Compose remove that implicit behavior and forces explicit state ownership, making architectural boundaries clear. 
	- `EditText` holds its own state
- Bugs were hidden 
### Compose 
- UI is pure function of state 
- It state is wrong  - UI is wrong 
### Benefit 
- Clarity in compose exposes mistakes fast  

## State Hoisting 
This make composable more reusable, testable and robust 
### Problem 
Storing mutable state directly in composable make it coupled to that specific component and it became harder to share. 
**Solution** - Move the state to a common parent or a `viewModel`
## Where to store 
- [[remember]]
- [[rememberSaveable]]
- [[derievedStateOf]]
