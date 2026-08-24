## `IntArray`
- `val squaresArray = Array(5) { i -> (i * i).toString() }`
	- `Creates an Array<String> with values ["0", "1", "4", "9", "16"]`
- `nums.sort()`

- Sort on existing object 
	- `usersArray.sortBy {it.salary}`
	- `usersArray.sortByDescending { it.name } `
- Sort returns new object
	- `usersArray.sortedBy { it.role }`
	- `usersArray.sortedByDescending { it.role }`
