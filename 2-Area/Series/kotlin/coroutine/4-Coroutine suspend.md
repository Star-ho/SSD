- coroutine의 suspend는 게임을 일시 중단하는 것과 유사함
	- 게임을 잠깐 중단했다가 resume하면 게임이 다시 시작됨
	- 이것은 suspend와 유사

```kotlin
suspend fun main() {
    println("Before")

    suspendCoroutine<Unit> { continuation ->
        continuation.resume(Unit)
    }

    println("After")
}
```
- suspend 만 있다면 중지되고 재시작되지 않음
- suspend 후 작업을 재개하려면 suspend 내에서 continuation을 resume을 호출해야함

```kotlin
private val executor =
    Executors.newSingleThreadScheduledExecutor {
        Thread(it, "scheduler").apply { isDaemon = true }
    }

suspend fun delay(timeMillis: Long): Unit =
    suspendCoroutine { cont ->
        executor.schedule({
            cont.resume(Unit)
        }, timeMillis, TimeUnit.MILLISECONDS)
    }

suspend fun main() {
    println("Before")

    delay(1000)

    println("After")
}
// Before
// (1 second delay)
// After
```
- 위 코드는 delay 함수의 간략한 구현임



https://kt.academy/article/cc-suspension