To save state with `ViewModel` use [[ViewModel#SavedHandleState]]
## Configuration Changes 
It happens when device configuration changes but process is still alive and healthy. It just recreates the activity. 
E.g.
- Screen rotation,
- Dark/Light Mode
- Multi-window resize
- Font scale change
- Locale/Language change.
**Same Process, Same memory (Singleton Objects), Same ViewModelStore**
[[ViewModel#Cases#Config changes]]

## What happen during Rotation
``` sequnce 
Activity running -> Configuration changes 
onPause() - onStop() - onSavedInstanceState()[best-effort] - onDestroy()

New Same Activity recreated 
restore save state
onCreate() - onStart() - onResume()
```
### Questions 
Q Why does Android recreate the activity instead of reuse it?
>Android’s resource system is **static at creation time**.
- Rotation triggers a configuration changes which affect 
	- Screen width / height 
	- Resource selection -  layout being inflated (`land` `port` in `res`), Drawables 
- What if we did reuse 
	- Updating existing activity will be fragile and error prone as it would require manually updating layout, reloading resources and managing existing view references.
	- It will increase complexity, error prone to developers, may cause inconsistent behavior across devices. 
	- Holding references to old view, could cause subtle leaks. 
- Why recreation helps 
	- Activity will ensure that correct resources are reloaded and applied. 
	- Android chooses Predictable correctness at the framework. Framework will behave consistent. 
	- Memory leaks would be less likely  


