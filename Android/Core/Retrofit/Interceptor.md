>Interceptor are the parts of OkHttp 

The reason is simple - if you want to add header (token) in every call then you can pass it through interceptor automatically. 

Otherwise you need to add it manually in every call. 
```kotlin 
@GET("path/path")
suspend fun getUser(
	@Header("Auth") token: String
): List<User>
```