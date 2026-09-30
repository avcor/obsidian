## Commit 
You can find that after using commit `fragment.isAdded` is false. It is not immediate.
``` kotlin 
private fun demonstrateCommit() {  
    Log.d(TAG, "--- demonstrateCommit() START ---")  
  
    supportFragmentManager.beginTransaction()  
        .replace(R.id.fragment_container, Fragment1(), "fragment1")  
        .addToBackStack("fragment1_transaction")  
        .commit()  
  
    Log.d(TAG, "commit() called - but Fragment1 may not be attached yet")  
  
    Log.d(TAG, "Fragment1 immediately after commit(): ${if (fragment?.isAdded == true) "ADDED" else "NOT ADDED YET"}")  
  
    Log.d(TAG, "--- demonstrateCommit() END ---")  
}
```

## CommitNow
You can find that using `commitNow()` `fragment.isAdded` is true. It is immediate
```kotlin
private fun demonstrateCommitNow() {  
    Log.d(TAG, "--- demonstrateCommitNow() START ---")  
  
    supportFragmentManager.beginTransaction()  
        .replace(R.id.fragment_container, Fragment2(), "fragment2")  
        // NOTE: Cannot use addToBackStack() with commitNow()!  
        // .addToBackStack("fragment2_transaction") // This would throw IllegalStateException        .commitNow()  
  
    Log.d(TAG, "commitNow() called - Fragment2 WILL be attached now")  
  
    // Fragment2 WILL be attached at this point because commitNow() is synchronous  
    val fragment = supportFragmentManager.findFragmentByTag("fragment2")  
    Log.d(TAG, "Fragment2 immediately after commitNow(): ${if (fragment?.isAdded == true) "ADDED" else "NOT ADDED"}")  
  
    Log.d(TAG, "--- demonstrateCommitNow() END ---")  
}
```

## CommitAllowingStateLoss 
When activity goes to background it will add the fragment to frame
``` kotlin 
private fun demonstrateCommitAllowingStateLoss() {  
    Log.d(TAG, "--- demonstrateCommitAllowingStateLoss() START ---")  
  
    // Simulating a delayed operation that might happen after onSaveInstanceState()  
    // This is common in async callbacks (network requests, database queries, etc.)    Handler(Looper.getMainLooper()).postDelayed({  
        try {  
            supportFragmentManager.beginTransaction()  
                .replace(R.id.fragment_container, Fragment1(), "fragment_delayed")  
                .commitAllowingStateLoss()  
  
            Log.d(TAG, "commitAllowingStateLoss() succeeded - even if called after onSaveInstanceState()")  
        } catch (e: Exception) {  
            Log.e(TAG, "Error: ${e.message}")  
        }  
    }, 5000) // 2 second delay  
  
    Log.d(TAG, "--- demonstrateCommitAllowingStateLoss() END ---")  
}
```