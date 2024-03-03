---
created: 2024-03-02T22:41:32
updated: 2024-03-03T11:41
---
### visualVM startup profiler 옵션
- startup profiler 설정시 필요한 옵션
	- 마지막 포트번호 변경될 수 있음
```
-agentpath:/Applications/VisualVM.app/Contents/Resources/visualvm/visualvm/lib/deployed/jdk16/mac/libprofilerinterface.jnilib=/Applications/VisualVM.app/Contents/Resources/visualvm/visualvm/lib,5140 
```
- profiler 관련 옵션
```
-Xshare:off
```

### 코루틴 디버깅 위한 옵션
```
-Dkotlinx.coroutines.debug
```