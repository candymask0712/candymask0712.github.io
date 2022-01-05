---
title: "[Computer Architecture] 컴퓨터 구조 - 5 - 논리회로와 데이터 표현"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Computer Architecture
tags:
  - logical gate
last_modified_at:
---

### **1. 컴퓨터에서의 데이터 표현**

- 디지털 정보의 단위

  - 1 nibble = 4 bit / 1 byte = 8bit / 1 byte = 영문자 1개
  - 1 워드 : 특정 CPU에서 사용하는 명령어나 데이터의 길이 (8의 배수)

- 진법과 진법변환

  - 2진법 : 0과1 두 가지 기호로 표현하는 수의 체계
  - 10진법 : 0~9 열 가지 기호로 표현하는 수의 체계
  - BCD code (Binary Coded Decimal Code) : 2진화 10진 코드

### **2. 보수**

- ons's complement : 최대값을 형성하는데 서로 보완 관계에 있는 두 수 사이의 관계
- 이진법에서 음수표현 & 뺄셈 연산에 보수의 개념을 활용

### **3. 논리 게이트(Logical gate)**

- 논리 연산을 수행하는 전자소자
- 입력 값에 대해 논리 함수 시행 => 함수의 연산 결과와 동일한 결과 출력하는 하드웨어
- 스위칭이론 : 스위치로 2진정보를 표현 & 논리연산 실행하도록 하는 이론

  - 스위치가 연결된 상태(1(X)) / 스위치가 연결되지 않은 상태(0(X'))
  - 스위치 이론에 논리적 구현 추가 : 직렬(AND), 병렬(OR)

### **4. 논리 연산의 기본 표현**

1. 논리 곱 (AND) : 입력 신호가 모두 참일 때 참을 출력
2. 논리 합 (OR) : 입력 신호 중 하나가 참일 때 참을 출력
3. 논리 부정 (NOT) : 입력 신호 참/거짓의 반대를 출력
4. 배타적 논리합 (exclusive OR) : 입력신호가 다를 때 참, 같을 때 거짓을 출력

[참고링크](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=cni1577&logNo=221619153912)
[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
