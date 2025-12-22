To save state with `ViewModel` use [[ViewModel - SavedStateHandle#SavedHandleState]]
## Configuration Changes 
It happens when device configuration changes but process is still alive and healthy. It just recreates the activity. 
E.g. Screen rotation, Dark/Light Mode, Multi-window resize, Font scale change, Locale change.
**Same Process, Same memory (Singleton Objects), Same ViewModelStore**
``` sequnce 
Activity running -> Configuration changes 
onPause() - onStop() - onDestroy()

New Same Activity recreated 
onCreate() - onStart() - onResume()
```
[[ViewModel - SavedStateHandle#Cases#Config changes]]
### Questions 
Q Why does Android recreate the activity instead of reuse it?
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

## Process death 
Android kills the app process to reclaim memory. It is an OS level kill so no [[Activity Lifecycle|lifecycle]] callbacks are called.
When process death happens entire heap is wiped
Triggers 
- App in background, could be Low memory 
- User switches app 
- System pressure 
``` sequence
App goes to background - Process Killed (Memory wiped)
User returns to app 
New process start - New Application - New Activity  
```
[[ViewModel - SavedStateHandle#Cases#Process death]]
### Questions 
Q Why not keep `ViewModel` across process death ?
- It is a memory construct, process - bound, lifecycle aware, UI state holder. 
- It's responsibility is to survive configuration changes, not process death. 
- When process death happens entire heap is wiped out, objects are gone, no lifecycle callback called.
	- Keep it would require entire object, restoring later. This is not view model is meant for. 
- Android must remain free to kill process instantly, reclaim memory aggressively, prioritize system responsiveness. If this would be requirement then android need to coordinate with app before killing them, which will make the process slow, because serializing comes at the cost which can cause the UI freezes or ANR. If you want to store small UI states then [[ViewModel - SavedStateHandle#Cases#Process death]] it is a better choice.
	- View models often hold non-serializable resources (Flow or coroutines), serializing them will hamper performance
	- Keeping view model will risk stale state or corrupted state. Explicit restoration is better  
