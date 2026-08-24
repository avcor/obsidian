- `val minStack = arrayListOf<Int>()`
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