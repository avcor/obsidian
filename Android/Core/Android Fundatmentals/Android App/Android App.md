- Android app is a **linux process** with a **main thread** hosting **android components**
- Activities are just object in those process 

## How application is loaded 

### What the user sees (System UI)
- Display starting screen [[#Starting-loading window]] for the app immediately after launch.
### Process initialization (Before app code)
1. **Process Creation**
	- [[Zygote]] forks a new process 
	- ART is attached 
	- Main (UI) thread is prepared 
	- App process is created with no Java/Kotlin objects 
2. **Content Providers initialization** 
	- All declared content provider are initialized 
	- Why it run before `Application.onCreate`
		- Some app data must be available immediately
		- Providers may be accessed by other apps
	- Heavy work in content provider -> slow cold start 
### App framework initialization (App code begins)
3. App class is loaded (`Application.onCreate`)
4. Launch Activity creation 
	- Instance is created 
	- `onCreate()` is called 
	- View hierarchy is inflated 
	- Measure & Layout the screen  
	- Perform initial draw 
5. First frame rendered 
	- App replaces the starting window 
	- App becomes visible and interactive

## Starting-loading window
Before android 12 - it was blank white or black screen 
Starting with android 12-  it screen created using app's launcher icon and defined app theme 