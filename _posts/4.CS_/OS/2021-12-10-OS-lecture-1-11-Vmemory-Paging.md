---
title: "[OS lecture 1] 운영체제 구조 - 11 - 가상 메모리"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - virtual memory
last_modified_at:
---

### **1. 가상 메모리**

- 메모리가 실제 메모리보다 많아 보이게 하는 기술
- 각 프로세스 마다 메모리 할당하기에 크기 한계 (리눅스 기준 4GB)
- 프로세스는 가상 주소를 사용하고, 사용시에만 물리주소에서 찾아 씀

### **2. MMU**

- 메모리 접근 필요시 가상 주소를 물리주소로 변환해 주는 장치
- 하드웨어 장치를 사용해야 주소변환이 빠르기에 MMU 필요
- CPU -- virtual address --> MMU -- physical address --> memory

### **3. 페이징 시스템**

- 크기가 동일한 페이지로 가상 주소 공간과 이에 매칭되는 물리주소 공간 관리
- 페이지 번호를 기반으로 가상/물리주고 매핑 정보를 기록
- 프로세스(4GB)의 PCB에 page table의 구조체를 가리키는 주소 존재
- page table에는 가상/물리주소의 매핑정보 있음(페이지번호 + 변위)

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
