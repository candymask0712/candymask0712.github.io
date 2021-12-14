---
title: "[OS lecture 1] 운영체제 구조 - 15 - 부팅의 이해"
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

### **1. 부팅**

- 컴퓨터를 켜서 동작시키는 절차
- Boot 프로그램

  - 운영체제 커널을 storage에서 특정 주소의 물리 메모리로 복사
  - 터널의 처음 샐행위치로 PC를 가져다 놓는 프로그램

### **2. 부팅 과정**

- 컴퓨터를 키면 BIOS가 특정 storage 읽어와 bootstrap loader를 메모리에 올리고 실행
- bootstrap loader 프로그램이 있는 곳을 찾아서 실행

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
