---
date: 2024-06-21 23:07:11
updatedAt: 2024-06-22 11:26:29
tags:
  - Stream
  - I/O
categories:
  - Concept
---
## Stream이란?
- 시간이 지남에 따라 잠재적으로 무제한으로 제공되는 데이터 요소의 시퀀스(연속)
- 데이터를 모두 불러온 뒤 처리하는것이 아닌, 데이터가 생성되는 즉시 처리할 수 있음
	- 컨베이어벨트 위의 항목이 대량으로 처리되는 것이 아니라, 벨트위의 항목 한번에 하나씩 처리

## 입출력(I/O)을 스트림(InputStream, OutputStream)으로 하는 이유
- InputStream, OutputStream의 목표는 다양한 입력과 출력을 추상화한 것
	- 데이터가 연속된것이기에 모든 유형의 데이터를 받을 수 있음
- 중요한것은 스트림이 파일인지 웹페이지 인지가 중요한것이 아닌, 스트림에서 데이터를 받거나, 주는것임





- https://en.wikipedia.org/wiki/Stream_(computing)
- https://stackoverflow.com/questions/28459498/why-are-java-streams-once-off