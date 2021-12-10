---
title: "[OS lecture 1] 운영체제 구조 - 10 - 교착상태/기아상태"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - deadlock
  - starvation
  - scheduling
last_modified_at:
---

### **1. 교착상태(Deadlock)**

- 무한 대기 상태 : 두 개 이상의 작업이 서로 상대의 작업이 끝나길 기다리고 있어 진행 불가
- 발생조건 : 상호배제/점유대기/비선점/순환대기의 조건이 모두 성립 시 발생
- 교착상태의 예방 : 앞선 네 가지 조건 중 하나를 제거함

### **2. 기아상태(starvation)**

- 특정 프로세스의 우선순위가 낮아서 자원을 계속 할당받지 못하는 상태
- 해결안 : 우선순위 변경 (우선순위 자주변경, 기다린 시간에 따른 우선순위, 요청순서 식 처리 등)

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
