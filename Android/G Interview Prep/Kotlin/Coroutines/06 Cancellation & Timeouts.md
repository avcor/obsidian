- `job.cancel()` to cancel manually
- `withTimeout()` or `withTimeoutOrNull()` for automatic cancellation
	throws `TimeoutCancellationException`

```kotlin
withTimeoutOrNull(3000) {
    repository.fetchUser() // if it takes more than 3s, cancel
} ?: println("Timeout")
```

