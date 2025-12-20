## `LifeCycle`
- It is an **abstract** class that tracks  lifecycle changes of a component
- [`lifecycleOwner`](#LifeCycleOwner) exposes it. `LiveData` / custom observer can react to it.  
- Uses 2 enumerations 
	1. Event 
		- dispatched from framework and lifecycle class 
		- these events map to callback events in activities and fragment
	2. State 
		- Current state of component 
``` kotlin
public abstract class Lifecycle {
    public enum State { INITIALIZED, CREATED, STARTED, RESUMED, DESTROYED }
    public enum Event { ON_CREATE, ON_START, ON_RESUME, ON_PAUSE, ON_STOP, ON_DESTROY, ON_ANY }
}
```

| **Transition (State Change)**           | **Event Trigger** | **Corresponding Activity/Fragment Method** |
| --------------------------------------- | ----------------- | ------------------------------------------ |
| **CREATED**                             | `ON_CREATE`       | `onCreate()`                               |
| **CREATED** $\rightarrow$ **STARTED**   | `ON_START`        | `onStart()`                                |
| **STARTED** $\rightarrow$ **RESUMED**   | `ON_RESUME`       | `onResume()`                               |
| **RESUMED** $\rightarrow$ **STARTED**   | `ON_PAUSE`        | `onPause()`                                |
| **STARTED** $\rightarrow$ **CREATED**   | `ON_STOP`         | `onStop()`                                 |
| **CREATED** $\rightarrow$ **DESTROYED** | `ON_DESTROY`      | `onDestroy()`                              |

## `LifeCycleOwner`
- Interface with single method (which must be implemented by class ) that denotes the class has a [[#`LifeCycle`|Lifecycle]]. 
- [[Activity#`ComponentActivity`|ComponentActivity]], `Fragment`, `ProcessLifeCycleOwner` all these implements this

```kotlin
public interface LifecycleOwner {
    fun getLifecycle(): Lifecycle
}
/*
lifecycle.addObserver(MyObserver())
it is possible because activity implements LifecycleOwner
*/
```

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

## `LifecycleRegistry`
- A concrete class that implements [`LifeCycle`](#Lifecycle)
- Responsible for managing observer, tracking state and dispatching lifecycle events 
- Used in internally in [[Activity#`ComponentActivity`|componentActivity]] and Fragment 
- *It act as brain behind lifecycle system - it updates state and notifies the observer*
