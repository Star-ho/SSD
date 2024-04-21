---
date: 2024-04-19T23:12:00
updatedAt: 2024-04-21 18:32:05+2650
tags: 
---
mysql의 col length는 charset과 무관하게 실제 저장 가능한 글자 수를 의미하고
실제 저장되는 사이즈는 charset의 바이트를 곱해야 합니다.
utf8의 경우 1char = 3byte, utb8mb4의 경우 1char = 4byte로 알고 있습니다.