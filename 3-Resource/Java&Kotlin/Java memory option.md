container에서 들어가야할 옵션들 정리

oom터졌을때 처리
memory관련 설정
- container메모리와 heap은 같은 사이즈로 가면 안됨
	- java에는 heap말고 non-heap도 있기때문
	- 컨테이너 메모리와 같은 양으로하면 컨테이너도 crash발생
- percentage로 75%정도 권장
	- ms홈페이지 참고
- 한컨테이너에 하나의 어플리케이션만 돌아갈떄 min size와 max size를 같게 설정
	- 메모리가 부족이 발생하면 os에 메모리를 더 달라고 요청한

**MaxRAMPercentage**
```ruby
UseContainerSupport
```

```ruby
CrashOnOutOfMemoryError
```


## 옵션들 보면서 어떤옵션인지, 확인하고 쓸만한것들 정리하기
