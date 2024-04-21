---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:52+8390
tags: 
---
## String 생성 방법
- new 연산자를 사용해서 생성하는 방법
	- String a = new String("abcd")
	- new 연산자로 생성하면 heap영역에 저장됨
- 리터럴로 생성하는 방법
	- String a = "abcd"
	- 리터럴로 생성한다면 컴파일시 String pool에 저장됨

## String pool?
- String이 저장되는 공간
- 컴파일될때 코드에 나타난 리터럴로 선언된 String들이 String pool에 들어감
- String을 '\=='으로 비교할때는 같은 객체인지를 확인함
	- new String("abcd")를 '\=='비교를 하면 "abcd"는 false임
	- 하지만 "abcd"와 "abcd"는 같음
	- 이유는 new String으로 생선된 String객체는 스트링 풀이 아닌, Heap에서 데이터를 가져오기 때문

- new String("abcd").intern() 을 사용하면 현재 스트링을 String pool에서 가져옴
	- String pool에 없다면 새로 생성함

https://deveric.tistory.com/123

#Java 