---
title: "[Computer Architecture] 컴퓨터 구조 - 8 - CPU 내부구조와 레지스터"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Computer Architecture
tags:
  - register
last_modified_at:
---

### **1. CPU의 구성요소**

- 중앙 처리 장치(Central Processing Unit)

  - 컴퓨터에서 데이터 처리동작을 수행하는 부분
  - 레지스터세트(register set) : 명령어를 실행에 필요한 데이터 보관
  - 산술논리장치(ALU, Arithmetic Logic Unit) : 명령어 실행위한 마이크로 연산 수행
  - 제어장치(Control Unit) : RS 간 정보저농 감시, ALU에게 수행할 동작 지시

### **2. 각 레지스터의 명칭/기능**

- 프로그램 계수기(PC, Program Counter)

  - 다음에 수행 될 명령어가 들어있는 주 기억장치의 주소를 기억
  - IC(instruction counter : 명령어 계수기) 혹은 LC(location counter : 위치계수기)라고도 부름

- 명령 레지스터(IR, instruction Register)

  - 프로그램 계수기(PC)가 지정하는 주소에 기억되는 명령어를 해독하기 위해 임시기억 역할

- 명령어 해독기(ID, Instruction Decoder)

  - IR에 들어 있는 명령코드 해석을 담당(명령코드 => 제어 신호화하여 기계 사이클로 전송)

- 제어장치(Control Unit)

  - ID가 보낸 신호에 따라 명령어 실행(clock에 의해 발생)

- 범용 레지스터(GPR, General Purpose Register)

  - 작업 레지스터에서 DATA가 용이하게 처리도도록 임시로 자료를 저장하는 경우 사용

- 작업 레지스터(Working Register)

  - 산술논리연산을 실행할 수 있도록 자료를 저장하고 결과를 저장하고

- 상태 레지스터(State Register)

  - CPU의 상태를 나타내는 특수목적의 레지스터
  - 연산결과의 상태, Z(zero), S(부호, sign), V(overflow), C(carry), I(Interrupt)

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
