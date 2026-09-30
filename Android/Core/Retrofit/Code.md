
``` kotlin 
interface MyApi {
	@GET("path/path")
	suspend fun getUser(): List<User>
}
```
^Interface

``` kotlin 
val retrofit = Retrofit.Builder()
	.baseUrl("https://website.com")
	.client(okHttpClient)
	.addConverterFactory(...)
	.build()
```
^retrofit-builder

```kotlin 
val api = retrofit.create(MyApi::class.java)
```
^api-class

```kotlin
val okHttpClient = OkHttpClient.Builder()
	.addInterceptor(AuthInterceptor())
	.build()
```
^okHttp-client

```kotlin
class AuthInterceptor: Interceptor {
	ovveride fun interceptor(chain: Interceptor.Chain) : Response {
		val request = chain.request()
			.newBuilder()
			.addHeader("Auth", "Token")
			.build()
			
		return chain.proceed(request)
	}
}
```