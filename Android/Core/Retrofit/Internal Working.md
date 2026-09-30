To call api we generally do
![[Code#^api-class]]

- It examines what is method, path, return type 
- Retrofit dynamically creates the implementation for interface.
- It construct the corresponding OkHttp request. 

Conceptually 
``` kotlin
class UserApiImplementation {
    fun getUsers(): List<User> {
        // Retrofit generated this logic
    }
}
```
