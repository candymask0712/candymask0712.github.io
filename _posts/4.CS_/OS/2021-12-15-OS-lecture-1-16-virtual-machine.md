---
title: "[OS lecture 1] 운영체제 구조 - 16 - 가상 머신"
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

### **1. 가상머신**

- 하나의 하드웨어에 다수의 운영체제 설치 => 개별 컴퓨터처럼 동작라도록 하는 프로그램
- 가상머신의 종류
  - type-1 : 운영 체제와 응용프로그램 하드웨어에서 분리
  - type-2 : 하이퍼바이저 또는 VMM이 Host OS 상위에 설치

### **2. 전가상화 VS 반가상화**

- 전가상화 : 각 가상머신이 하이퍼바이저를 통해 하드웨어와 통신 (KVM)
- 반가상화 : 각 가상머신이 직접 하드웨어와 통신 (VM Ware)

### **3. 가성 머신 VS Docker**

- 가상 머신 : 컴퓨터 하드웨터를 가상화 (하드웨어 전체 추상화)
- Docker : 운영체제 레벨에서 별도로 분리 된 실행환경 제공 (커널 추상화)

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
