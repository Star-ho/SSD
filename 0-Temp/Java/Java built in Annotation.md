java의 built in Annotation은
**@Deprecated**
**@Override**
**@SuppressWarnings**
**@SafeVarargs**
**@FunctionalInterface**
이 있고,

다른 어노테이션에 붙을 수 있는 어노테이션은
**@Retention**
**@Documented**
**@Target**
**@Inherited**
**@Repeatable**
이 있다

이 중 Retention의 정확한 의미가 와닿지 않아 정리해 보겠다.

# Retention
---
```
Indicates how long annotations with the annotated interface are to be retained
```
-> annotation이 얼마나 유지되는 정도를 나타냄, 디폴트는 Class
### Source
- 컴파일될때 사라짐

## Class
- 클래스파일에는 기록되지만, vm에 올라갈떄 사라짐
 
## Runtime
- 클래스파일에도 기록되고, vm에 올라감
- 

> Class vs Runtime
@Lorg/example/RetentionSourceAnnotation;() // invisible <- Class
@Lorg/example/RetentionSourceAnnotation;() <- Runtime
but


위 세가지가 무엇을 의미하는가?
Runtime은 vm에 올라가니 reflection으로 확인이 가능한데 Source와 Class는 무슨 차이인가?




https://docs.oracle.com/javase/tutorial/java/annotations/predefined.html


#Annotation