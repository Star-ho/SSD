### Memory
- 정확한 크기로 설정
	- -Xmx(ex -Xmx4g), -Xms(ex -Xms500m)
- 비율로 설정
- container메모리와 heap은 같은 사이즈로 가면 안됨
	- java에는 heap말고 non-heap도 있기때문
	- 컨테이너 메모리와 같은 크기로 했을 때 컨테이너도 crash 발생하기 때문에 oom 후처리가 안됨
- percentage로 75%정도 권장
	- [ms홈페이지 참고](https://learn.microsoft.com/en-us/azure/developer/java/containers/overview)
	- 물론 절대적인건 아님
- 한컨테이너에 하나의 어플리케이션만 돌아갈떄 min size와 max size를 같게 설정
	- 메모리가 부족이 발생하면 os에 메모리를 더 달라고 요청하는데, 어차피 하나의 컨테이너에 하나의 프로세스만 돌아가는데 굳이 필요없는 요청을 늘릴 필요가없음
	- gc가 더 많이 돔

**MaxRAMPercentage**
```ruby
UseContainerSupport
```

```ruby
CrashOnOutOfMemoryError
```


## 옵션들 보면서 어떤옵션인지, 확인하고 쓸만한것들 정리하기


#wait-to-update 