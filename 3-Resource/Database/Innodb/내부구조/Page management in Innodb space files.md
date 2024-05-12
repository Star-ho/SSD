---
date: 2024-05-12 17:45:54
updatedAt: 2024-05-12 17:46:17
---

## Extent
- 64개의 연속된 페이지인 1MiB블록
- space에서 페이지를 관리하려면 복잡하기에, 중간에 Extent를 두어 space는 Extent를 관리하고, Extent에서 page를 관리
- Innodb는 FSD_HDR과 XDES페이지를 고정된 위치에 두어 extent가 사용중인지, extent내의 사용중인 페이지를 추적함

### FSP_HDR/XDES 구조
![center](Pasted%20image%2020240512174953.png)
- FIL Header와 trailer, FSP Header와 256개의 extent discriptors(EHSMS descriptors)가 포함됨
	- 많은 양의 미사용공간도 포함됨

### Extent decriptor
![center](Pasted%20image%2020240512175239.png)
- File Segment ID : extent가 파일 세그먼트에 속할시시, extent가 속한 파일 세그먼트 id, 



## List - free list
- 여러 관련 구조를 함께 연결할 수 있는 일반적인 구조체
### List base node
- 하이레벨구조(FSP헤더와 같은)에서 한번만 저장됨
- 리스트의 길이 및 리스트의 처음과 마지막 리스트 노드의 정보를 포함함

### List Node
- 이전과 다음 노드에 대한 포인터를 저장함

- 모든 포인터는 페이지 번호(같은 space내에 있는)와 리스트 노드를 찾을 수 있는 해당 페이지 내의 byte offset으로 구성됨
- 모든 포인터는 리스트 노드의 시작을 가르킴
- 반드시 서로 연결된 구조는 아님


## 파일 segment INODE
- INODE페이지에는 85개의 파일 segment INODE항목(16KiB)이 포함되어 있으며 각각 192bytes임
- 다음 INODE페이지 리스트에 사용되는 리스트 노드가 포함되어 있음
