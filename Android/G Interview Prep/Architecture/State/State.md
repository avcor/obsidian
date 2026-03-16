- Any information that affects what user sees or what system does.
- State is meaningful information that represent the system at a point of time. 
- If it changes - behavior or UI changes 
- Android forces you to separate the state - because of fragile environment
## Key properties 
- Deterministic 
- Re playable 
- Serializable 
- Testable 
## UI state 
> UI state is the projection of domain state, optimized for rendering.
- State that exists only to render the UI
- It is cheap to recreate 
-  Losing it does not break the correctness
-  Example 
	- Selected tab
	- Checkbox checked
	- Expanded / Collapsed state
- If UI state is lost, user may be annoyed but app is still correct. 
## Domain State
- State represent the business truth 
- Has meaning even if UI does not exist 
- Must survive in every condition usually backed by persistence or  backend. 
- Examples 
	- Logged in user 
	- Feature flags 
	- Sync Status 
- Losing it causes incorrect behavior 
> Domain state is the source of truth. UI state is derived from it. 
## Compose-specific
- UI state = `remember`, `rememberSaveable`
- Domain state = Flow / State Flow from repository
> [[Compose]] makes state boundaries visible. It does not fix bad architecture.

## How to decide state 
- If this is lost, app is still correct ?
- Does this define business truth ?
- Who is allowed to change ?
- What is its  ?