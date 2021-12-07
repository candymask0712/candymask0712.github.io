---
title: "[OS lecture 1] 운영체제 구조 - 12 - 페이징시스템"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - virtual memory
  - paging
last_modified_at:
---

### **1. 다중 단계 페이징 시스템**

    - 페이징 정보를 단계를 나누어 생성 (필요없는 페이지는 생성X)
    - 페이지 번호를 나타내는 bit 구분해 단계를 나눔

### **2. TLB**

    - TLB(Translation Lookaside Buffer) : 페이지 정보 캐쉬
    - 한 번 접근하여 변환된 물리주소 정보 저장 (속도 빠름)

### **3. 공유 메모리**

    - 프로세스 간 동일한 물리주소 가르킴 (공간 절약, 메모리 할당 시간 절약)
    - 리눅스 기준 프로세스마다 할당 된 kernel의 3~4GB 공간의 물리주소는 동일

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
