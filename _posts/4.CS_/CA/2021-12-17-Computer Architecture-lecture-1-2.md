---
title: "[Computer Architecture] 컴퓨터 구조 - 2 - 컴퓨터 구조로 본 패러다임의 변화"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Computer Architecture
tags:
  - CPU
last_modified_at:
---

### **1. 중앙처리장치 (Central Processing Unit)**

1. CPU

   - 실행 프로그램의 명령 해석, 실행, 장치 제어
   - 산술 논리 연산장치(ALU), 제어장치(CU), 각종 레지스터로 구성

2. MPU(Micro Processor Unit)

   - CPU를 고밀도 집적회로화(LIS)한 일종의 통합 장치

3. H/W 플랫폼 종류

   - 아두이노 등 사물 인터넷 디바이스 종류도 존재

### **2. 주변장치 (Peripheral Device)**

1. 기억장치 (Memory unit)

   - RAM (Random Access Memory)

     - 컴퓨터를 종료하면 데이터가 날아가는 휘발성(리프레쉬)
     - DRAM(Dynamic)과 SRAM(Static)으로 나뉨

   - ROM (Read Only Memory)

2. 보조기억장치

   - 동작속도는 느리나 가격이 저렴하고 다량의 데이터 저장

3. 주 기억장치와 보조기억 장치의 관계

   1. 부팅시 CPU는 ROM에 있는 프로그램 실행
   2. CPU는 메모리로부터 실행할 명령어와 데이터를 가져와 처리
   3. RAM는 보조기억장치에 저장(save)하고, 보조기억장치는 RAM에 적재(load)함

4. 입/출력장치(input/Output device)

    - I/O기기라고 부르며 키보드, 마우스, 스캐너 등 다양한 장치들

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
