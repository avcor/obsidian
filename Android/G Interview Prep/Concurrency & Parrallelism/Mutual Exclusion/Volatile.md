Concurrent programming has memory model which governs when writes becomes visible across threads. 

Volatile does not make increment safe like `++`.

```kotlin
var running = true
// thread A
running = false

// thread B
while (running) {
    // work
} 

// In this code you cannot say when thread B wil see it. 
```

## Annotation
``` kotlin
@Volatile 
var running = true
```

Another way - [[Atomic Variables]]

