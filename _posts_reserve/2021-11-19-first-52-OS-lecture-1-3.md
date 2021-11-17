---
title: "[OS lecture 1] 운영체제 구조 - 3 - 스케쥴링 알고리즘"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - process
  - scheduler
last_modified_at:
---

### **1. 프로세스(process)**

- 메모리에 올려져서 실행 중인 프로그램
- 작업, 테스크, job이라는 용어와 혼용해서 사용 됨
- 응용프로그램 !== 프로세스(응용프로그램은 여러 프로세스로 이루어 질 수 있음- IPC기법 등)

### **2. 스케쥴링 알고리즘**

- 스케쥴러(scheduler) : 프로세스 실행을 관리
- 스케쥴링 알고리즘 : 목표에 따라 어떤 순서대로 프로세스를 실행할 지 결정
- 시분할(응답 시간을 짧게), 멀티 프로그래밍(CPU 활용도 높히기)

### **3. 기본 스케쥴러**

1. FIFO 스케쥴러

   - 프로세스가 다른 작업 없이 CPU를 처음부터 끝까지 사용
   - 가장 간단 / 배치 처리 시스템 / FCFS(First Come First Serve) - 큐

2. 최단 작업 우선(SJF) 스케쥴러

   - SJF(Shortest Job First) : 가장 실행시간이 짧은 프로세스 부터 먼저 실행
   - 실행시간이 예측 가능한 경우가 많은 RealTime OS와 관련 깊음(공장, 공정)

3. 우선 순위 기반(Priority-Based) 스케쥴러

   - 정적 우선순위 (프로그램마다 우선순위 미리 지정)
   - 동적 우선순위 (스케쥴러가 상황에 따라 우선순위 변경)

4. Round Robin(RR) 스케쥴러

   - 작업이 남았아도 단위시간 실행 후 ready queue로 들어감 -> 순서가 되면 다시 실행
   - 시분할 시스템을 기반으로 작동

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
