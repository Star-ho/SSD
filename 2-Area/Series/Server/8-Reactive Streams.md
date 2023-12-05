## 개념
- 논블로킹 배압(back pressuer)을 사용한 비동기 스트리밍 처리를 위한 표준
- network protocol 뿐만아니라 JVM, Javascript와 같은 런타임 환경에 대한 표준도 포함함
- 스트림 데이터라고도 표현되는 크기가 정해지지 않은 'live'데이터는 비동기 시스템에서 주의가 필요함
	- 들어오는 데이터가 처리되는 속도보다 빠르면 안되기 때문
		- 데이터가 많으면 쌓이고, 그러다 보면 메모리가 터지기때문
- Reactive Streams의 주요 목표는 비동기 경계를 넘은 데이터 스트림의 교환(데이터를 다른쓰레드 혹은 쓰레드 풀로 전달하는)하며 수신측에서는 임의의 데이터양을 버퍼로 관리하지 않는것임
- backpressure는 스레드 사이의 대기열을 제한하기 위한 필수적인 부분임
- 또한 백프레셔 신호가 동기식일 경우 비동기 처리의 이점이 없어지기에, Reactive Streams의 구현은 모든측면에서 비차단, 비동기식으로 구성되도록 주의를 기울임

## 구성요소

- Publisher는 잠재적으로 무한한 수의 시퀀스 요소를 제공하며, Subscriber의 요청을 받으면 요소를 제공하기 시작함
- `Publisher.subscribe(Subscriber)`에 대한 응답으로 Subscriber는 아래의 신호를 받음```
```
onSubscribe onNext* (onError | onComplete)?
```
- Publisher.subscribe를 호출하면, 반드시 한번 onSubscribe가 호출되며, 무한한 onNext를 방출
- 이후 Subscription이 cancel되지 않으면, 에러가 발생하면 onError, 더 이상 전달할 요소가 없다면 onComplete를 호출
	- Subscription이 cancel되면 onError, onComplete를 호출하지 않을 수 있음

> 어떻게 구현해야 하는지에 대한 설명으로, 필자는 구현보다는 사용에 관한 관점에 대해 정리함
> 너무 구현에 관한 설명에 대해서는 작성하지 않으므로 구현내용이 궁금하다면 [링크](https://github.com/reactive-streams/reactive-streams-jvm/blob/v1.0.4/README.md)를 참조
### Publisher
```
public interface Publisher<T> {
    public void subscribe(Subscriber<? super T> s);
}
```
- 무한한 시퀀스 요소를 Subscriber에게 제공
- publisher는 요청된 수만큼, 혹은 요청된 수보다 적은 onNext를 호출해야함
- 요청된 수보다 적은 onNext를 보내고, onError 혹은 onCompelete로 구독의 종료를 알릴 수 있음
- 에러발생시 onError, 더이상 전달한 요소가 없다면 onComplete를 반드시 호출해야함
- Subscriber에게 onError 혹은 onComplete를 보낼 시, Subscriber는 해당 Subscription을 취소된 것으로 간주해야함
- 종료신호(onError 혹은 onComplete)를 보낸 후에는 더이상 신호가 발생하지 않아야함
- Publisher가 subscribe호출을 받으면 반드시 Subscriber의 onSubscribe을 호출해야함
	- 제공된 구독자가 null인 상황에서는 NullPointerException예외를 던져야함
	- 제공된 구독자가 null이 아닌 상황에서는 정상적으로 응답해야함

### Subscriber
```
public interface Subscriber<T> {
    public void onSubscribe(Subscription s);
    public void onNext(T t);
    public void onError(Throwable t);
    public void onComplete();
}
```
- onNext 신호를 받기위해서는 반드시 Subscription.request(long n)신호를 보내야함
- onComplete() 및 onError(Throwable t)는 신호를 수신한다면 구독이 취소된것으로 간주해야함
- Subscriber가 이미 활성화된 Subscription을 가지고 있을때, 새로운 Subscription을 받는다면 새로운 Subscription에 대해 cancel을 호출해야함
	- Subscriber는 반드시 하나의 Publisher를 가져야함
- Subscription이 더 이상 필요하지 않다면 Subscriber는 cancel을 호출해야함
- Subscriber는 반드시 Subscription의 request와 cancel이 순차적으로 호출되도록 보장해야함

### Subscription

https://www.reactive-streams.org/
https://github.com/reactive-streams/reactive-streams-jvm/blob/v1.0.4/README.md