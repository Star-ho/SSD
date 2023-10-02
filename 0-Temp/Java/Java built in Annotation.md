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
- 런타임시 리플렉션으로 정보를 가져올 수 없음
 
## Runtime
- 클래스파일에도 기록되고, vm에 올라감
- 런타임시 리플렉션으로 정보를 가져올 수 있음


> Source vs Class
> 	Source는 컴파일된 바이트 코드에서 아예 보이지 않음
> 	Class는 보이지만 invisible이라는 주석이 붙음
> 	라이브러리를 만들때 

> Class vs Runtime
> 	@Lorg/example/RetentionSourceAnnotation;() // invisible <- Class
> 	@Lorg/example/RetentionSourceAnnotation;() <- Runtime
> 	bytecode를 보면 RetentionPolicy가 Class일때 컴파일된 코드에서 invisible이라는 주석이 붙음
> 	주석이 따로 기능을 할지.. 궁금하다...
> 		추가자료 
> 		https://www.javassist.org/html/javassist/bytecode/AnnotationsAttribute.html


https://docs.oracle.com/javase/tutorial/java/annotations/predefined.html
https://minkukjo.github.io/language/2020/09/30/Java-02/

#Annotation