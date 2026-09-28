Atomic operations allow multiple threads safely read and modify shared state without using traditional lock.

```kotlin
val counter = AtomicInteger(0)
counter.incrementAndGet()
```

`incrementAndGet` act as one indivisible operations.

*Thread cannot observe a half completed increment from Thread A.*

``` kotlin
// Warning
// not thread safe
if (counter.get() < 10) {
    counter.incrementAndGet()
}
```

[How it works internally](https://chatgpt.com/share/6ab5639c-8044-83e8-ab59-8ca93cbcc041)
