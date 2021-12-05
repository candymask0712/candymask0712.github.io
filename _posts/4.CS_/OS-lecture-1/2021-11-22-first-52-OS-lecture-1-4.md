---
title: "[OS lecture 1] 운영체제 구조 - 4 - 프로세스 상태와 스케쥴링"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - process
  - scheduling
last_modified_at:
---

### **1. 프로세스의 3가지 상태**

- 멀티 프로그래밍 : CPU 활용도를 극대화하는 스케쥴링
- runnung state : 현재 CPU에서 실행 상태
- ready state : 현재 CPU에서 실행 가능 상태
- block state : 특정 이벤트 발생 대기 상태

### **2. 선점형과 비선점형 스케쥴러**

- 비선점형 : 프로세스가 자발적으로 block state 또는 실행이 끝냈을 때만 프로세스 교체 가능
- 선점형 : 프로세스가 running state에 있어도 스케쥴러가 중단시키고 다른 프로세스로 교체 가능
- 선점형은 한 작업이 오래걸리더라도 프로세스 교체 가능 (사용자 입장 반응속도 빠름)

### **3. 스케쥴러의 구분**

- FIFO(FCFS), SJF, Priority-Based는 어떤 프로세스를 먼저 실행시킬지에 대한 알고리즘 (비선점형에 가까움)
- Round-Robin(RR)은 시분할 시스템을 위한 기본 알고리즘(선점형 스케쥴러)

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
