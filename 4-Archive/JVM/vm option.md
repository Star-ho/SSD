---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:53+1750
tags: 
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