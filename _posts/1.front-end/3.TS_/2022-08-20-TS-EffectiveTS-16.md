---
title: "[TypeScript] Effective TS - item.16 number 인덱스 시그니처 대신 좋은 대안 사용하기"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - Effective TS
last_modified_at:
---


### **1. 배열은 객체이므로 키는 숫자가 아니라 문자열**

- 배열은 객체이므로 키는 숫자가 아니라 문자열
- 따라서 문자열 키를 이용해도 배열 요소에 접근 가능

  ```javascript
  // 배열의 키로 문자열 사용 가능 (keys 사용 시에도 문자로 출력)
  x = [1, 2, 3]
  x[0] // 1
  x['0'] // 1
  Object.keys(x) // [ '0', '1', '2' ]

  for(const key in x){
    key // key는 string
    const tmp = x[key] // 배열의 Index는 number 타입이나 에러 발생X(TS의 실용적 허용)
  }
  ```
### **2. 인덱스 시그니처에 number 대신 좋은 대안을 사용하기** 


