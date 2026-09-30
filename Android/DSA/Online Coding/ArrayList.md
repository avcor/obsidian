- `val minStack = arrayListOf<Int>()`
- `list.add(0,"lol")`
- `minStack.lastOrNull()`
- `removeLast()` Exception thrown `NoSuchElementException`
- `positionSpeed.sortByDescending {it.position}`
- `users.sortWith { a, b -> a-b}`

- Sort on same reference  ```
```
list.sortWith(
    compareBy<Event> { it.size }
        .thenBy { it.end }
)
```