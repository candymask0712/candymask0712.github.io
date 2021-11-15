---
title: "[OS lecture 1] 운영체제 구조 - 1 - 커널모드 & 시스템 콜 "
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - OS lecture 1
tags:
  - shell
  - system call
last_modified_at:
---

### **1. 시스템콜(system call)**

- 운영체제는 사용자 인터페이스 제공

  - 쉘(shell) : 사용자가 운영체제 기능 조작할 수 있는 인터페이스 제공
  - 터미널 환경(CLI) / GUI 환경으로 구분

- 운영체제는 응용프로그램을 위한 인터페이스 제공

  - API(Application Programming Interface) : 함수로 제공 (open() 등)
  - 보통은 라이브러리(library) 형태로 제공 (C library 등)
  - 시스템콜 : OS의 기능 사용을 위해 OS가 제공하는 명령 또는 함수
  - **프로그램이 OS 기능 요청을 위해 시스템콜을 이용해 만든 API 사용**

### **2. 커널 모드(kernel mode)**

![OS 내부의 권한계층](https://github.com/candymask0712/candymask0712.github.io/blob/master/_posts/images/2021-11-15-image.png?raw=true)

- CPU의 권한모드 (CPU Protection Ring)

  - 사용자 모드 : 응용프로그램이 사용
  - 커널모드 : OS가 사용 (특권명령어 실행 & 자원접근 가능)

- 시스템콜은 커널모드로 실행

  - 커널모드에서만 가능한 기능 -> 커널모드 실행 시 반드시 시스템콜 거쳐야 함
  - **OS기능 쓰는 API호출 시 커널모드로 변경 -> OS 내부에서 실행 후 응용프로그램으로 돌아감**

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
