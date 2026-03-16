>A repository exist to centralize source of truth for domain state and coordinate among multiple data sources.
>It owns consistency rule for domain data and prevent UI-scoped components from owning long-lived business rule. 
>**Not an abstraction layer**
## Characteristics
- Should be mock able or fake able 
- Should Expose deterministic behavior 
- Should not require Android Framework behavior 
- Centralizes concurrency control
## Problem
- Invariant Violation (UI)
	- UI layer decides domain strategies, (caching, refresh, upload). Now every screen can have different rules. System becomes non-deterministic. 
- Multiple Source of truth 
	- If data fetching strategies are in ViewModel then every ViewModel decides independently. At scale there will be inconsistency. 
- If UI or ViewModel is directly contact with data source such as Network APIs, or local db, any change in how data is fetched forces changes in higher layers. This tightly couples UI logic with the infrastructure concerns, making system fragile, bug prone. A repository acts as an stable boundary that absorbs the changes and keep upper layer unaffected. 
### Solving
- It answer to the questions such as 
	- Should we fetch from network or cache ?
	- What happens if network fail ?
- It not just hide implementation, it enforces data policies 
	- Such as 
		- Offline vs online first 
		- Retry behavior 
		- Fallback logic 
	- If these rules are scattered across ViewModel or UI, system becomes unpredictable. 

## When Overkill 
- App is purely read only 
- No Business rule
- No coordination required
- No consistency rules

## Per Entity vs Per Feature
>Choice depends on whether the data relationship or feature behavior is dominant source of complexity.
### Per Entity 
- You create repository for every database table or entity. (*when relatively independent*)
- Repository contains all the logic for specific data type, regardless of where that data is used in app.
- Vibe - Everything related to 'User' goes in 'User' file.
- Pros 
	- Logic for user is centralized in one place.
- Cons 
	- Over time, file becomes massive because adding every query needed for that entity. 
	- It is like one size fits for all.
	- Multiple entities must be coordinated. 
### Per Feature 
- You create repository tailored for a specific screen or business process.
- Vibe - Only add exactly those feature which are required to do its job. 
- Pros 
	- Highly decoupled - changes in one flow wont affect other flow
	- Optimized for that particular screen.
	- Feature isolation and provide reasoning for that behavior. 
- Cons 
	- Code duplication.
	- Less reuse across the feature.
	- It can be harder to get big picture of how entity is handled across entire system. 
