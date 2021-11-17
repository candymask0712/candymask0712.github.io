---
title: "[OS lecture 1] 운영체제 구조 - 2 - 프로세스 스케쥴링"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - batch processing
  - time sharing system
  - multi tasking
last_modified_at:
---

### **1. 배치 처리 시스템(batch processing)**

- 실행 요청 순서에 따라 프로그램을 순차적으로 실행(FIFO)
- 한 번에 등록 된 여러 프로그램을 순차실행 가능
- 단점 : 큰 작업 시 다른 작업 지연 / 동시 실행 불가 / 다중 사용자 불가

### **2. 시분할 시스템(time sharing system)**

- 다중 사용자 지원을 위해 컴퓨터 응답 시간을 최소화하는 시스템
- CPU의 전체 사용시간을 작은 시간량으로 쪼재 작업을 할당/처리

### **3. 멀티 태스킹(multi-tasking)**

- 단일 CPU에서 여러 프로그램이 동시에 실행되는 것처럼 보이게 하는 시스템
- 시분할 시스템을 기반으로 작동

### **4. 멀티 프로세싱(multi-processing)**

- 여러 CPU에서 하나의 프로그램을 병렬로 실행하여 실행속도를 극대화

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
