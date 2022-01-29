---
title: "[Computer Architecture] 컴퓨터 구조 - 10 - 마이크로연산과 ALU"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Computer Architecture
tags:
  - ALU
last_modified_at:
---

### **1. 마이크로 연산**

레지스터에 저장 된 데이터에 대해 수행되는 기본적 연산

1. 전송 마이크로 연산 : 레지스터 사이에서 이진 정보 전송
2. 산술 마이크로 연산 : 레지스터에 저장 된 수치 데이터 대해 산술 연산 수행
3. 논리 마이크로 연산 : 레지스터에 저장 된 비수치 데이터에 대해 비트 조작 연산 수행
4. 시프트 마이크로 연산 : 레지스터에 저장 된 데이터에 대핸 시프트 연산을 수행

ALU는 산술 연산과 논리 연산을 처리

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
