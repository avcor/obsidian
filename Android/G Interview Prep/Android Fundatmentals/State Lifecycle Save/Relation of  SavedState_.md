- [[SavedStateRegistry]] - engine
- [[SavedStateRegistryOwner]] - who host the engine 
- [[SavedStateHandle]] - high level api build on top of engine (but does not extend or implement) for `ViewModel` 

``` 
AppCompactActivity 
| 
FragmentActivity 
| 
ComponentActivity 
|
SavedStateRegistryOwner (interface)
|
SavedStateRegistry
```

