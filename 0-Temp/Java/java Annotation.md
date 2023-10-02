java annotation을 만들때 타겟은 어노테이션이 붙는 타겟을 의미하는데 리텐션의 의미가 궁금해 정리해보았다.

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

위 세가지가 무엇을 의미하는가?
Runtime은 vm에 올라가니 reflection



#Annotation