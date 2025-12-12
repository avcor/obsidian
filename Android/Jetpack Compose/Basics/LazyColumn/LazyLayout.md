`LazyColumn` /  `LazyRow`
## Keys or Item Identity 
- The key is unique, stable identifier for each item in the list. 
- By default it uses the index as identifier.
- Compose tracks the specific composable associated with that key even when list content or order changes. 
### If use index as key 
When item is moved compose sees another composable at that place & recomposes and measures it again instead of moving the existing item.
## How it works 
It is efficient because it only composes and lay out items that are currently visible on screen, plus few items right before and after visible view port as buffer. 
## Practice 
### Bad practice
- Prevent nested lazy scrolling
  E.g. `LazyColumn` inside another `LazyColumn` without fixed height for inner one   
### Good practice
- If you have header or footer you can use `item{}` so that it could be measure only once 

## Optimization 
- Check for image size - Use library to load images such as glide or Koil
- Keys 
- Use layout Inspector to know how many times the composable are rendered 
- `data class` (auto stable) 
- `@Immutable` annotation (if all fields are val)
- `@Stable` for custom behavior