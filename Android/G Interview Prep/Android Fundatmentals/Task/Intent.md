Intent is a messaging object that is used to request action from another app component (same).
Use cases 
- Starting a activity 
- Starting a service 
- Delivering a broadcast 
## Explicit Intent 
Specify which component of which application will satisfy the intent by specifying full component name. You will use this to start component in your app, because you know class name or service name. 
## Implicit Intent 
Do not know specific component name but instead declare general action to perform, which allow component from another app to handle it. 
Caution - Security 
- Do not put intent filters in service at manifest you would not be to know which app started your service.
- It is advised to specify the component name when starting the service. Otherwise you wouldn't be certain which service has started.
### Working 
Android find appropriate component to start by comparing the intent content passed to intent filter of other apps declared in manifest file. 
- If it finds the component then it will start the activity or multiple component are found then dialog is shown. 
- If not found it will throw exception `ActivityNotFoundException`
	- How to prevent 
		- Verify before call `myIntent.resolveActivity(packageManager) != null` it returns `ComponentName`
		- Try Catch
**Intent Filters** - it is an expression that specify type of intent it would like to receive. 

## Building an Intent 
- **Component Name** - component to start 
	- `Intent(this, MyAct.class.java)`
	- `myIntent.setComponent()`
- **Action** - define action to perform 
	- `ACTION_VIEW` or `ACTION_SEND`
- **Data** - define the URI to be acted upon, you can use `setType()` to  add MIME type. 
	- `setData()` & `setType()` will nullify each other 
	- `setDataAndType()`
- **Category** 
- **Extra** - Key - value pair to add additional information. 
	- `putExtra`
- **Flags** - meta data for intent. Flag instruct system how to launch an activity. Different flags are defined in [[Intent Flags]]
