[[02 Suspend|Suspend]] will return a single value, **Flow** will return multiple values
## Cold Flow 
- Data is emitted when there is collector, Every collector gets its own fresh data stream 
- Fetching list from network call, best when you need to emit multiple values in Offline-First project.

## Hot Stream 
- Data is emitted regardless of collector
- late collector can miss the emission
### Types 
- `SharedFlow` / `MutableSharedFlow`
	- Broadcast to multiple collector 
	- It has replay value
	- Does not require initial value
- `StateFlow` / `MutableStateFlow`
	- Holds a current value (similar to liveData) 
	- Similar to Shared Flow 
#### TODO
`shareIn`
`Eagerly`
`WhileSubscribed`
`Lazily`

