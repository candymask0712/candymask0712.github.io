---
title: "[CleanCode] 클린코드 공부하기 - 4 - 주석"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - CleanCode
  - comment
tags:
  - CleanCode

last_modified_at:
---

## **1. 코드를 보조하는 주석**

### 1. 주석을 최대한 쓰지 말자

- 나쁜 주석

  - 코드에 주석을 추가하는 주 이유는 코드 품질 문제
  - 주석으로 설명하는 대신 코드로 의도를 표현해야 함
  - 주석은 방치 된다 (컴파일 되지 않기에)
  - 따라서 사람을 거쳐가며 의미없는 텍스트가 됨

  ```javascript
  // 이름만으로는 의도를 파악할 수 없음
  if((employee.flag & HOURLY_FLAG ) && employ.age > 65)
  
  // 의미있는 이름을 지어 해결 (직원이 복지 혜택 받을 수 있는지)
  if(employee.isEligibleForFullBenefit())
  ```

- 좋은 주석

  - 구현에 대한 정보 제공
    ```javascript
    // 가독성이 떨어지는 정규식에 대한 정보 제공
      
    // kk:mm:ss EEE, MMM dd, yyyy 형식
    Pattern timeFormat = 
      Pattern.compile("\\d*:\\d:\\d* \\w*, \\w* \\d* \\d*")  
    ```
  - 의도와 중요성을 설명 (현업에서 자주 사용)
    ```javascript
    // 스레드를 많이 생성하여 시스템에 영향을 끼치는 테스트
      
    for (int = 0; i <25000; i++) {
      someThread someThread = ThreadBuilder.builder().build();
    }
      
    // 유저로부터 입력받을 값을 저장할 때 trim으로 공백제거 필요
    String username = userNameInput.trim();
    ```
  - TODO, FIXME 주석
    - TODO: 앞으로 할 일
    - FIXME: 문제가 있지만 당장 수정할 필요는 없을 때

  - 주석보다 annotation 사용
    - annotation: 코드에 대한 메타데이터
    - @Deprecated: 컴파일러가 warning 발생 (IDE 사용 시 표시)
