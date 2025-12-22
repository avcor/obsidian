- It is a coordination mechanism that allows multiple independent component to contribute there small pieces of state into a single saved-state snapshot, and restore them later. 
- It is owned by activity / fragment 
- Used by child components 
## Why exist 
### Problem earlier
- There was only one bundle `onSaveInstanceStat(outState: Bundle?)` and everyone competed for it - views, fragment , libraries.
- Problem it faced 
	- key collision 
	- no owner ship clarity
- Android needs decentralized state saving and central snapshotting


