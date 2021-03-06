---
title: "[OS lecture 1] 운영체제 구조 - 7 - IPC"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - IPC
  - process
  - scheduling
last_modified_at:
---

### **1. IPC**

- 프로세스는 다른 프로세스의 공간 접근 불가 (해킹 위험)
- IPC(InterProcess Communication) : 프로세스 간 통신방법 제공
- 처리 속도를 위해 병렬처리 시 IPC가 필수

### **2. IPC의 커뮤니케이션 방법**

- file 사용 : 저장매체를 거쳐야 해서 실시간 처리 어려움
- kernel 사용 : 공유 공간인 kernel을 이용해 실시간 처리

### **3. 주요 IPC 기법**

1. 파이프 (pipe)

   - 기본 파이프 구조는 단방향 통신
   - fork() 로 자식프로세스 만들어 부모->자식으로 통신

2. 메세지 큐 (message queue)

   - FIFO 방식으로 데이터 전송 (먼저 넣은 데이터 먼저 읽힘)
   - 부모자식 간 아닌 모든 프로세스간 통신 가능

3. 공유메모리 (shared memory)

   - kernel에 메모리 공간 만들고 해당 공간을 변수처럼 사용
   - 공유 메모리 KEY를 가지고 여러 프로세스가 접근 가능

### **4. 주요 IPC 기법 - 2 (IPC 외 사용)**

- 시그널과 소켓 방식은 IPC기법이지만 이 외에도 많이 사용 됨

1. 시그널 (signal)

   - 커널 또는 프로세스에서 다른 프로세스에 어떤 이벤트 발생했는지 알려줌
   - 프로세스에 시그널 핸들러 등록해 해당 시그널 처리
   - PCB에 해당 프로세스가 처리해야 하는 시그널 관련 정보 관리
   - SIGKILL(프로세스죽이기), SIGSTP(프로세스 멈추기) 등

2. 소켓 (socket)

   - 두 개의 다른 컴퓨터 간 네트워크 통신 기술 (서버-클라이언트 등)
   - 하나의 컴퓨터 안에서 프로세스 간 통신 기법으로 사용 가능

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
