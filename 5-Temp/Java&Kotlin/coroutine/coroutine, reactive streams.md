coroutine에서는 어떻게 reactive streams를 지원할까?

https://github.com/Kotlin/kotlinx.coroutines/blob/master/reactive/kotlinx-coroutines-reactive/src/Await.kt#L183


await하는 메서드들은 내부적으로 awaitOne을 호출하는데
awaitOne메서드 내부에서 subscribe를 호출함

https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-reactive/


#Kotlin 
#Reactive-Streams
#Coroutine