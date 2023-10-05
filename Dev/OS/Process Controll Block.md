```embed
title: "[운영체제]PCB (Process Control Block)란? PCB 정보 & Context Switching 문맥교환 & Overhead 오버헤드"
image: "https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9954F44E5C51D43939"
description: "운영체제 목차 프로세스의 정의와 프로세스 상태에 대한 이해를 기반으로 하고 있습니다. 헷갈리시는 분은 이전 포스팅 보고 오기 프로세스를 조금 어렵게(?) 이렇게 표현하기도 해요 프로세스는 프로세서에 의해 수행되는 프로그램 단위로 현재 실행 중이거나 곧 실행 가능한 PCB(Process Control Block)을 가진 프로그램이다. 음.. PCB가 프로세스와 관련된 건 알겠는데 PCB는 무엇을 의미할까요? PCB (Process Control Block)란? ♣ 운영체제가 프로세스를 제어하기 위해 정보를 저장해 놓는 곳으로, 프로세…"
url: "https://jhnyang.tistory.com/33"
```

### PCB
>프로세스 제어 블록(Process Control Block, PCB)는 운영체제에서 중요한 정보를 저장하는 <font color="#9c86e9">**자료구조**</font>이다. 
>PCB는 프로세스의 실행 상태를 관리하고, 스케줄링, 멀티태스킹, 문맥 교환(Context Switching) 등의 작업을 수행하는 데 필요한 정보를 포함하고 있다.


![[Pasted image 20231005231431.png]]
PCB는 다음과 같은 항목을 포함하고 있다.
- **Process Id**: 프로세스의 고유 번호
- **Process State**: ready, wait, running 등의 실행 상태