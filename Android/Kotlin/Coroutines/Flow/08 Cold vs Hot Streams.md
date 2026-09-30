[[02 Suspend|Suspend]] will return a single value, **Flow** will return multiple values
## Cold Stream
- Data is emitted when there is collector, Every collector gets its own fresh data stream 
- Fetching list from network call, best when you need to emit multiple values in Offline-First project.
## Hot Stream 
- Data is emitted regardless of collector
- late collector can miss the emission
*`BroadCastChannels`it is replaced by `SharedFlow`*
### Types 
- [[Channels]]
- [[SharedFlow]]
- [[StateFlow]]
## [[08.1 Flow vs Channels |Flow vs channel]]

