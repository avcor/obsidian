Offline First 
```kotlin
sealed class Resource<T>(
    val data: T? = null,
    val message: String? = null
) {
    class Success<T>(data: T) : Resource<T>(data)
    class Loading<T>(data: T? = null) : Resource<T>(data)
    class Error<T>(exception: Throwable, data: T? = null) :
        Resource<T>(data, exception.message)
}
```

```kotlin
class UserRepository(
    private val api: UserApi,
    private val dao: UserDao
) {
    fun getUsers(): Flow<Resource<List<User>>> = flow {
        // Step 1️⃣: Emit cached data first
        val cached = dao.getAllUsers()
        emit(Resource.Success(cached))

        // Step 2️⃣: Emit Loading state (to show progress indicator)
        emit(Resource.Loading(cached))

        // Step 3️⃣: Fetch fresh data from network
        try {
            val fresh = api.getUsers()
            dao.insertAll(fresh)
            emit(Resource.Success(fresh)) // New updated data
        } catch (e: Exception) {
            // Step 4️⃣: Emit Error state, still show cached data
            emit(Resource.Error(e, cached))
        }
    }.flowOn(Dispatchers.IO)
}
```

```kotlin
class UserViewModel(
    private val repository: UserRepository
) : ViewModel() {

    // 1️⃣ Refresh trigger — emits whenever user clicks refresh
    private val refreshTrigger = MutableSharedFlow<Unit>(
        replay = 1, // keep last trigger for new collectors
        extraBufferCapacity = 1
    )

    // 2️⃣ Transform trigger into actual data stream
    val users: StateFlow<List<User>> = refreshTrigger
        .flatMapLatest {
            repository.fetchUsers() // new network call each refresh
                .onStart { println("Fetching users...") }
                .catch { emit(emptyList()) } // handle error gracefully
        }
        .stateIn(
            scope = viewModelScope,
            started = SharingStarted.WhileSubscribed(5000),
            initialValue = emptyList()
        )

    // 3️⃣ Call this when user presses refresh
    fun refresh() {
        refreshTrigger.tryEmit(Unit)
    }
}
```
