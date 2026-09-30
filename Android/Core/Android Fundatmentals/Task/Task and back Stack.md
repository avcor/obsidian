A task is a collection of activities that user interacts.
**System behavior changes in > & <= android 11**
StudentForm
When user clicks on the app icon it creates a task with containing activities. Which can go to foreground and background. 
### Manages Task 
There are attributes for managing tasks 
Flags for intent modes 
### Define launch modes 
#### Using Manifest 
- Standard
	default mode. one task can have multiple instance of activity
- SingleTop 
	If instance of an activity is at top of a task, new request is directed to onNewIntent() instead of creating new one. 
	That is not applicable for a instance which is not at the top then new instance will be created. In the this case there could be multiple instance each instance could belong to different task. 
- SingleTask 
	System create a new instance at the root of new stack or find the activity in an existing task with same [[#taskAffinity | affinity]] . If exist it will route with onNewIntent() without new instance. Meanwhile destroying all other activities being destroyed on top. 
- SingeInstance
	Similar to single task. Activity is the only member of task, if new activity is created then it will be new task. e.g. Incoming call UI or floating video player
	which effectively allows _just one_ instance across the whole system/task universe
- SingleInstancePerTask 
	Activity is the root of the task, and there could be only one instance of that activity in that task. Eg document editing activity for different documents   

#### Using intent flag 
- FLAG_ACTIVITY_NEW_TASK 
	Similar to SingleTask
- FLAG_ACTIVITY_SINGLE_TOP
	Similar to SingleTop
- FLAG_ACTIVITY_CLEAR_TOP
	If activity is running in current task, then system will destroy all activities on top and deliver intent through onNewIntent() without launching a new instance.
	No Similar thing can be found in launchMode Manifest.
### Handle Affinity
- FLAG_ACTIVITY_NEW_TASK flag 
- allowTaskReparenting
	Even the activity started in one app's task it could be later claimed into task which it truly belonged

### Clear back stack 
Default behavior - if user leaves the  task for a long time then system clear all the activities in the task except for the root activity. 
To modify this behavior using activity attributes 
1. alwaysRetainTaskState 
	retain all the activities in the task even after long period
2. clearTaskOnLaunch
	task is cleared down to root activity whenever user leaves the task and return to it. 
3. finishOnTaskLaunch
	it only remove the single activity if user leaves and returns back. 

### Start a Task 
Activity that start there own task (like singleTask) should always have launcher entry 
```
<activity ... >
    <intent-filter ... >
        <action android:name="android.intent.action.MAIN" />
        <activity ... >
    <intent-filter ... >
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
    ...
</activity><category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
    ...
</activity>
```
Android create app icon for this in app launcher 
If activity is singleTask it will launch in different task that's fine but if activity does not have launcher icon, and when user leaves the activity by pressing home button it could not get it back. It is actually orphaned - it is still in memory but unable to retrieve back through normal UI navigation. 

Use singleTask modes only for activities that has MAIN + LAUNCHER intent filter 

If you do not want user to return to screen you  can use `android:finishOnTaskLaunch="true"` task will be there but activity is removed, making sure that user gets fresh start. This is good for temporary screens, login confirmation or flows that need to be reset at each time. 