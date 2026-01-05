Go through [[Lifecycle - aware components]]
It is important to understand that first activity is not completely stopped before second one is created. If two activities are in same process then 
A `onPause()` - B `onCreate()` `onStart()` `onResume()` - A `onStop()`
## onCreate()
- Startup logic that happens only once for entire lifecycle of activity. Associate the activity with a `ViewModel`, instantiate some class scoped variable and inflate some views. 
- Receives [[Save Instance|savedInstanceState]] if new null otherwise bundle from previously saved state.
## onStart()
- App prepare the activity to enter foreground and become interactive 
- It is needed because when activity goes fully hidden & then comes back to foreground it need to come `onStart()` 
### Uses 
- Initialize listeners such as camera and check for permission.
- Good places to start animation that should run as soon as user sees the screen. 
## onResume()
- Activity comes to foreground and remains in this state until it goes away from focus.
- In Split screen mode two apps are visible but only one has user's focus 
- LifeCycle aware component receives ON_RESUME
### Uses 
- If user has focus then only start camera preview 
## onPause()
- Activity is no longer in foreground because of multi mode window does not have focus or dialog came foreground. 
- It does not offer enough time frame to to save user data, make network calls or execute database transactions. Use `onStop` for this. In a high pressure environment android can kill your background thread before finishes its work. 
## onStop()
- When activity is no longer visible or new activity covers the entire screen also when it finishes running and about to be terminated. 
- Activity object is kept resident in memory maintaining all states and member information. 
- It offers better time to save information in db 
## onDestory()
- It is called before the activity is destroyed
	- User dismissing the activity or `finish()` is being called
	- Due to configuration changes rotation or entering multi-window mode 
- User `viewModel.onCleared()` if activity is not being recreated. 
- Use `isFinishing()` can be used to distinguish between the recreation or destroyed 
- It is not guaranteed that it will be called if system tries to kill the process, due to memory constraints, when app is in background.
