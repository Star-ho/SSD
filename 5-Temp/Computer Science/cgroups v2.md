---
date: 2024-03-31T22:41:00
updatedAt: 2024-04-21 18:32:05+2520
tags: 
---
cgroup 메모리 초과 시 실행되고 있는 프로세스 중 메모리를 가장 크게 잡아먹는 프로세스를 kill함

When a cgroup goes over its limit, we first try to reclaim memory from the cgroup so as to make space for the new pages that the cgroup has touched. If the reclaim is unsuccessful, an OOM routine is invoked to select and kill the bulkiest task in the cgroup.

https://docs.kernel.org/admin-guide/cgroup-v2.html
#wait-to-update 