## Why Fragment exist 
- One Activity represent one screen, when user navigate activity switches 
- Tablets needs multiple panel
- Fragments are sub controller inside an activity.
	- Activity owns window, task, system focus
	- Fragments owns portion of UI + its logic
- Fragments in activities 
	- Allow one activity to host many screens 
	- Reusable navigation container
### problem will activities
- One Activity represent one screen, when user navigate activity switches 
- They could not be nested, share window.

## Observe in Fragment 
- Fragment Context 
	- `liveData.observe(this) { updateUI() }`
	- Observer tied to fragment lifecycle, fragment may be live and view may be destroyed
- View Context 
	- `liveData.observe(viewLifecycleOwner) { updateUI() }`
	- Observer may be destroyed at `onDestroyView()`
	- Safe across back stack & Config changes 
