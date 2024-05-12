---
date: 2024-05-12 17:45:54
updatedAt: 2024-05-12 23:22:08
---

## Extent
- 64개의 연속된 페이지인 1MiB블록
- space에서 페이지를 관리하려면 복잡하기에, 중간에 Extent를 두어 space는 Extent를 관리하고, Extent에서 page를 관리
- Innodb는 FSD_HDR과 XDES페이지를 고정된 위치에 두어 extent가 사용중인지, extent내의 사용중인 페이지를 추적함

### FSP_HDR/XDES 구조 요약
![center](Pasted%20image%2020240512174953.png)
- FIL Header와 trailer, FSP Header와 256개의 extent discriptors(EHSMS descriptors)가 포함됨
	- 많은 양의 미사용공간도 포함됨
- 아래에 더 자세한 설명 있음

### Extent decriptor
![center](Pasted%20image%2020240512175239.png)
- File Segment ID
	- extent가 파일 세그먼트에 속할시, extent가 속한 파일 세그먼트 id
- List node for XDES list
	- double linked extent descriptor 목록의 이전 및 다음 extent를 가르키는 포인터
- State
	- extent의 현재 상태를 나타냄(4가지 상태가 있음)
		- 해당 extent가 동일한 space목록에 속하는 FREE, FREE_FRAG, FULL_FRAG 상태
			- 아래에서 자세한 설명
		- 해당 extent가 파일 세그먼트 ID필드에 저장된 ID를 가진 파일 세그먼트에 속함을 의미하는 FSEG상태
- Page State Bitmap
	- 2개의 비트로 페이지의 패이지가 free한지, clean 한지 나타냄
		- 첫번빼 비트는 페이지가 free한지 여부
		- 두번째 비트는 clean한지 여부
			- 현재 사용되지 않는다면 1로 할당됨
- extent를 참조하는 다른 구조에서는 extent's descriptor가 있는 FSP_HDR 또는 XDES 페이지 번호와, descriptor entry가 존재하는 페이지의 byte offset을 조합하여 위치를 나타냄
	- page 0 offset 150은 첫번째 페이지에서 150번째 오프셋의 XDES Entry를 참조
		- 0-63페이지를 가지고 있는 XDES Entry임
	- page 16384 offset 270은 16384페이지에서 270번째 오프셋의 XDES Entry를 참조
		- 16576-16639페이지를 가지고 있는 XDES Entry임
		- page 16384는 실제로 첫 번째 XDES 페이지를 의미함



## List - free list
- List는 여러 관련 구조를 함께 연결할 수 있는 일반적인 구조체
- 2개의 상호보완적인 구조를 사용해서, 디스크상의 이중 링크드 리스트를 구현함
### List base node
![center](Pasted%20image%2020240512201648.png)
- 하이레벨구조(FSP헤더와 같은)에서 한번만 저장됨
- 리스트의 길이 및 리스트의 처음과 마지막 리스트 노드의 정보를 포함함

### List Node
![center](Pasted%20image%2020240512201700.png)
- 이전과 다음 노드에 대한 포인터를 저장함
- 모든 포인터는 페이지 번호(같은 space내에 있는)와 리스트 노드를 찾을 수 있는 해당 페이지 내의 byte offset으로 구성됨
- 모든 포인터는 리스트 노드의 시작을 가르킴
- 반드시 서로 연결된 구조는 아님

## FSP Header 상세
![center](Pasted%20image%2020240512201947.png)
- Space ID
	- 현재 space의 ID
- Highest page number in the space (size)
	- 파일이 커짐에 따라, 증가되는 유효한 최대 페이지 수
	- space확장은 여러 단계에 걸쳐 이루어지므로, 모든 페이지가 초기화 되지 않음(일부는 0으로 채워질 수 있음)
- Highest page number initialized (free limit)
	- FIL헤더가 초기화된 가장 높은 페이지 번호로, 페이지자체에 페이지 번호를 저장함
	- free lmit은 항상 이 크기보다 작거나 같음
- Flags
	- space와 연관된 플래그
- Next Unused Segment ID
	- 다음에 할당될 파일 세그먼트에 사용될 파일 세그먼트 ID
- Number of pages used in the FREE_FRAG list
	- 목록의 모든 extents를 순회하지 않고 FREE_FRAG갯수를 확인할 수 있게하기 위한 필드
- 다음 extent descriptor list의 List base node도 저장됨
	- FREE_FRAG
		- 여유페이지가 남아있는 extent를 나타냄
			- 여유 페이지가 있는 extent는 개별 페이지를 다른 용도로 사용 가능함
		- 예를들어, FSP_HDR 이나 XDES 페이지가 있는 모든 extent는 FREE_FRAG 목록에 배치뒤어 남은 free page를 다른 용도로 할당할 수 있음
	- FULL_FRAG
		- FREE_FRAG와 똑같지만, 여유페이지가 없는 extent를 나타냄
		- extent가 가득차면 FULL_FRAG로 이동되며, 페이지가 해제되어 가득차 있지 않으면 FREE_FRAG로 이동됨
	- FREE
		- 완전히 사용되지 않고, 특정 용도로 전체 할당할 수 있는 extent를 의미함
		- FREE extent는 파일세그먼트(적절한 INODE 목록에 배치되기 위해)에 할당되거나, 개별 페이지 사용을 위해 FREE_FRAG목록이로 이동될 수 있음
## file segment, INODE
- InnoDB는 파일시스템에서 사용하는 file segment, INODE를 오버로드해서 사용함
- InnoDB는 inode를 다음 2가지 유형에 사용함
	- INODE entires(하나의 작은 구조)
	- INODE pages(많은 INODE 항목을 포함하는 페이지 유형)
- InnoDB의 INODE는 단순히 file segment(FSEG)를 설명할 뿐이며, 앞으로 "file segment INODE"라 칭함


### INODE pages
![center](Pasted%20image%2020240512220333.png)

- 각각의 INODE page는 85개의 file segment INODE entries(총 16KiB page)를 포함함
	- 각각의 INODE page는 192바이트임
- INODE page는 FSP_HDR의 FSP 헤더 구조에서 설명했던 List node가 있음
	- 해당 List node는 INODE pages를 위한 것, 해당 INODE page의 INODE가 아님!
	- FREE_INODES
		- 적어도 하나의 free file segment INODE entry가 있는 INODE pages의 리스트
	- FULL_INODES
		- free file segment INODE entry가 하나도 없는 INODE pages의 리스트
		- file per table space를 사용하는 경우, 테이블에 42개 이상의 인덱스가 없는 한 각 file per table space 안에 있는 해당 목록은 비어있음
			- 각각의 index는 정확히 두개의 file segment INODE entry를 사용하기 때문
### INODE ENTRY
![center](Pasted%20image%2020240512231201.png)
- File Segment ID
	- file segment ID는 해당 file segment INODE entry를 의미함
		- ID가 0이면 해당 entry는 사용되지 않은 것을 의미
	- Magic Number
		- 값이 97937874이면 file segment INODE entry가 초기화 되었다는 것을 의미
	- Number of used pages in the NOT_FULL list
		- space의 FREE_FLAG list(FSP header에 있는)와 정확히 같음
		- NOT_FULL 리스트 수 빠르게 확인할 수 있게 하기 위한 필드
	- Fragment Array
		- space에 있는 FREE_FAG 또는 FULL_FRAG "fagment"의 extent리스트의 extent에 개별적으로 할당된 32페이지의 배열의 요소
		- 해당 array가 꽉 차면, 오직 full extents만 file segment에 할당될 수 있음



참고
https://blog.jcole.us/2013/01/04/page-management-in-innodb-space-files/