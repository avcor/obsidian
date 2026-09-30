`MutableSharedFlow`

- Broadcast to multiple collector 
- It has replay value
- Does not require initial value

## `shareIn`
It converts [[Flow|cold flow]] in hot Flow 
```kotlin 
fun <T> Flow<T>.shareIn(
    scope: CoroutineScope,
    started: SharingStarted, // This is where Eagerly, WhileSubscribed, or Lazily goes
    replay: Int = 0 // How many recent values to replay to new collectors
): SharedFlow<T>
``` 
### `SharingStarted`

|       | Eagerly                                | Lazily                                 | WhileSubscribed                                                                                             |
| ----- | -------------------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Start | Immediately                            | First collector starts collecting      | First collector starts collecting. Restart if previous collector completes flow and new one comes after it. |
| Stop  | Never. Live as long as scope is active | Never. Live as long as scope is active | When last collector stop collecting, `stopTimeout` to delay stopping                                        |


