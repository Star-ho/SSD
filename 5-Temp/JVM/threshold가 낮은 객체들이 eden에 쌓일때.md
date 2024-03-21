---
created: 2024-03-21T23:22
updated: 2024-03-21T23:23
---
안녕하세요 Java Garbage Collection에서 질문있습니다!

새로운 객체가 eden 영역부터 쌓이고, eden이 가득 차면 minor GC가 실행되어서 reachable한 객체들이 survivor 0,1 영역을 바꿔가며 쌓이는걸로 알고 있는데요,

궁금한건 survivor 영역이 age threshold를 넘지 못하는 reachable 객체로 가득 차버리는 상황이 발생하면 어떻게 되나요?

제가 생각했을때는 뭔가 age threshold가 낮아져서 survivor 영역에 가득찬 객체들을 old 영역으로 넘겨주거나 survivor 영역을 늘려주지 않을까 싶은데.. 어떻게 될지 궁금합니다

---
https://stackoverflow.com/questions/25887715/java-gc-how-is-desired-survivor-size-calculated

---

제가 정확하게 이해한 건지 모르겠지만 JVM에 의해 정해진 survivor 영역을 초과하는 순간 threshold 를 낮추는 것 같아요!

Desired survivor space means the max survivor space used by the live objects after each Minor GC, which is calculated by SURVIVOR_SPACE * TargetSurvivorRatio / 100, so you get half of the survivor space by default. If the size of live object exceeds the desired survivor space, JVM will reduce the threshold to force some objects to be moved to old generation in the next GC.

https://www.oracle.com/java/technologies/