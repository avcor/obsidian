## `DefaultLifeCycleObserver`
Interface that can monitor the component lifecycle status by implementing it. 

**why "default"** because it has empty implementation of each method, so you override only ones that you care about
`@OnLifecycleEvent` is deprecated

```kotlin
class MyObserver : DefaultLifecycleObserver {
    override fun onResume(owner: LifecycleOwner) {connect()}
    override fun onPause(owner: LifecycleOwner) {disconnect()}
}
myLifecycleOwner.getLifecycle().addObserver(MyObserver())
```
