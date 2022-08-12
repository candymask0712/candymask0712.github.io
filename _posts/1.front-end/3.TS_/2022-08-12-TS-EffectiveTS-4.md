---
title: "[TypeScript] Effective TS - item.04 - 구조적 타이핑에 익숙해지기 "
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

### **1. 타입 일치 시 세부 사항은 신경쓰지 않음**

- 다른 interface 라도 필요 요소의 타입 일치 시 가능 (구조적 타이핑)
- 필요한 요소 외에 추가 요소가 있더라도 오류 발생 X (타입은 open)

  ```javascript
  interface twoElement {
    a: number
    b: number
  }

  interface threeElement {
    a: number
    b: number
    other: number
  }

  const Func = (v: twoElement) => v.a + v.b

  // 함수 선언 시와 다른 interface를 전달
  const threeElementObj = { a:1, b:2, c:'apple' }
  // interface 간 관계 명시 X => 문제없이 실행 됨
  console.log(Func(threeElementObj)) // 3
  ```

  '구조적'타이핑이라는 용어가 이해를 어렵게 하는 듯..(구조가 달라도 인식하기 때문에)
  이해를 위해서는 '실용적' 타이핑 정도로 생각하면 어떨까..?

  - 추가 요소를 허용하기에 객체 순회 시 문제 사례

  ```javascript
  (...)
  const FuncLoop = (v: threeElement) => {
    for (const el of Object.keys(v)) {
      // 에러발생 -  (...) 'string' can't be used to index type 'threeElement'
      // el에 number 타입만 들어오는 것으로 타이핑이 되었지만
      // 추가요소인 d가 string값을 가지고 있기 때문
      const tmp = v[el]
      (...)
    }
  }

  FuncLoop({ a: 1, b: 2, c: 3, d: 'abc' })
  ```

  - 추가 요소 허용으로 인한 객체 순회 문제점 해결법

  ```javascript
  (...)
  function FuncLoop(v: threeElement) {
    // 아래와 같이 객체 순회가 아닌 객체의 요소 나열로 해결 가능
    // ()...이건 너무 하드코딩에 가까운 해결책이 아닌지?)
    return v.a + v.b + v.c
  }
  ```
