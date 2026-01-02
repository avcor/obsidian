Fragment have 2 lifecycle - object and view 
## Why android need this 
Because navigation demands this 
- Fragment A -> Fragment B. A is put on back stack 
- Android keep A's state & destroy A' view to save memory 
## Scenarios of crash 
Generally developer do this `lateinit var binding: FragmentExampleBinding` 
Fragment goes to back stack, `onDestoryView()` run and views are destroyed, binding still points to dead view. 
### Fix
Anything using view should live in `onCreateView()` and `ondestoryView()`
`binding = null` is needed

## Fragment Back Stack 
Activity Back Stack - Managed by Android, Each entry = Activity, Controlled by intent & launch modes 
Fragment Back Stack - Managed by `FragmentManager`, lives inside the activity. Explicit opt in `addToBackStack()`
### what happens
Fragment instance kept in memory - View are destroyed - lifecycle goes to `onDestroyView()`.
When user presses back - Fragment is popped, View is recreated, Fragment object is reused. 
#### Why this design 
- **Views are expensive to store in memory** - because it consist of bitmap, object of Views, and list. This will put pressure on memory, GC will run more often. There are chances that it will cause the process death & App restart, which will make app unpredictable. (XML parsing will also take CPU cycles)
- **State object are cheaper to store**  - because they would be view model fields, data classes, list which are pure memory objects. No UI work, Zero CPU cycle, but it will take some memory.
- **Also navigation needs to be faster** - destroying the old views frees up memory, creating new views are predictable cost. Recreating views is cheaper than keeping them in memory over time. Memory pressure is more dangerous than CPU spikes 