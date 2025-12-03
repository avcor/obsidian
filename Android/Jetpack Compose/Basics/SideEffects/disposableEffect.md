It is a side effect that needs cleanup, when the composable leaves the composition or one of the key is changed. 

## Lifecycle 
It launches the effect and then register the cleanup block (`onDispose` block)
## Uses
- Observing an observer, Managing the subscription, registering listeners 

```kotlin 
@Composable
fun LifeCycleObserver(
	onCreate: (()-> Unit)? = null
	onResume:(() -> Unit)? = null
	//... all others 
) {
	val lifecycleOwner = LocalLifeCycleOwner.current
	
	DisposableEffect(Unit) {
		val lifecycleObserver = LifecycleEventObserver { _, event -> 
			when(event) {
				LifecycleEvent.Event.OnCreate -> onCreate?.invoke
				LifecycleEvent.Event.OnResume -> onResume?.invole 
				// ... all others
			}
		}
		lifecycleOwner.lifecycle.addObserver(lifecycleObserver)
		
		onDispose {
			lifecycleOwner.lifecycle.removeObserver(lifecycleOwner)	
		}
	}
}


```