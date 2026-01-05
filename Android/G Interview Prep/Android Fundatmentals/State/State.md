Any data that influence what the user sees or can do. It influences the UI. 
## 4 Lifetime of state 
### 1. Composable Lifetime 
- Exists only while composable is composition 
### 2. Configuration changes 
- Survives rotation changes 
- Does not survive process death 
- E.g. 
	- `ViewModel`
	- [[rememberSaveable]] -  survives both config and process death
### 3.  Process death lifetime 
- Survive graceful OS killing app
- E.g. 
	- [[Save Instance]] 
	- [[rememberSaveable]]
### 4. App lifetime / Persistent 
- Survive app restart 
- Stored on disk 
- Logged in User, Cached Data 

## Handling in compose 
[[State in compose]]
