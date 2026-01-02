It is an object wrapper around Intent object. The purpose of it is to grant permission to foreign application to use Intent as it ware executed to from your own app.
### Use case 
- Declaring Intent when user performs an action with your notification.
- Declaring Intent to be executed when user performs an action with your app widget 
- Declaring Intent to be executed at specific future time (using `AlarmManager`)

### Static methods 
- `getActivity()` - start the activity
- `getService()` - start the service
- `getForegroundService()` - start foreground service
- `getBroadcast()` - send a broadcast signal 
### Security
When creating a pending intent, you must specify the flag to dictate how system handles it. 
- `FLAG_IMMUTABLE` 
- `FLAG_MUTABLE`
It did not specified then it will throw `IllegalArgumentException`