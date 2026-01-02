It is a an interface, implemented by `ComponentActivity`, `Fragment` 
```kotlin
interface SavedStateRegistryOwner {
    fun getSavedStateRegistry(): SavedStateRegistry
}
```

This is not optional 
If you want saved-state support, it must be hosted by owner 
No owner -> no registry -> no saved state 