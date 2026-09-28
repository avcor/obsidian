This prevent the threads to access the particular block at same time. 

- lock - It is simple object that is used to monitor that threads are synchronised on. Take it as key to the door.
- `synchronized(lock)` - Act as the room 

```kotlin
// you can use `this` instead of lock, which will refer to the object instance, 
synchronized(lock) { counter++ }
```

## Use of 2 locks 
```kotlin 
class Bank {

    private val accountLock = Any()
    private val transactionLock = Any()

    private var balance = 0
    private val transactions = mutableListOf<String>()

    fun updateBalance(amount: Int) {
        synchronized(accountLock) {
            balance += amount
        }
    }

    fun addTransaction(transaction: String) {
        synchronized(transactionLock) {
            transactions.add(transaction)
        }
    }
}
```


## [Synchronised - why locks are used & deadlocks](https://chatgpt.com/share/6ab52dfd-eb14-83e9-b32a-580c012ab705) 