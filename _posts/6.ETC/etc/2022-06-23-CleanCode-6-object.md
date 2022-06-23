---
title: "[CleanCode] 클린코드 공부하기 - 6 - 객체와 자료구조"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - CleanCode
  - object
  - data structure
tags:
  - CleanCode

last_modified_at:
---

## **1. 객체와 자료 구조로 데이터 표현하기**

### 1. 자료구조 vs 객체

  | 자료구조     | 겍체          |
  |-------------|----|
  | 데이터 그 자체 | 비지니스 로직과 관련 |
  | 자료를 공개        | 자료를 숨기고 추상화 |

- 자료구조
  - 자료구조 사용 시 절차적인 코드
  - 구조 변경 없이 새 함수 추가 쉽다
  - 새로운 자료 구조 추가가 어렵다 (모든 함수 수정 필요)

- 객체 지향 코드
  - 기존 함수 변경 없이 새 클래스 추가 쉬움
  - 새로운 함수 추가 어려움 (모든 클래스 수정 필요)

### 2. 객체 - 디미터의 법칙

![image](https://user-images.githubusercontent.com/86667412/175301980-e41c032d-29f0-4017-a90c-f4158a0948c1.png)

- 클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다

  - 클래스 C
  - 자신이 생성한 객체
  - 자신의 인수로 넘어온 객체
  - C 인스턴스 변수에 저장 된 객체

  ```javascript
    // case 1) 객체일 경우 - 기차 출동 발생 (디미터의 법칙 위배)
    final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
  
    // case 2) 자료 구조일 경우 - 가능
    final String outputDir = ctxt.options.scratchDir.absolutePath;
    
    // case 3) getter를 사용 시 - 좋은 방법이 아님
    // getter를 통했을 뿐 값을 가져오는 것은 자료구조
  
    ctxt.getAbsolutePathOfScratchDirectoryOption();
    ctxt.getScratchDirectoryOption().getAbsolutePath();
    
    // case 4) 절대 경로로 가져오기
    // 겍체는 자료를 숨기고 자료를 다루는 함수만 공개
    BufferedOputputStream bos = ctxt.createScratchFileStream(classFileName);
  ```

### 3. DTO (Data Transfer Object)

- 다른 계층 간 데이터를 교환할 때 사용
  
  - 로직 없이 필드만 가짐
  - 일반적으로 클래스명이 Dto(or DTO)로 끝남
  - getter/setter를 갖기도 함
  - Beans
    - Java Beans: 데이터 표현이 목적인 자바 객체
    - 멤버 변수는 private 속성
    - getter와 setter를 가짐