---
title: "[TypeScript] Effective TS - item.12 함수 표현식에 타입 적용"
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

### **1. 함수 표현식 전체에 타입 구문 적용이 좋은 방식**

- JS에서는 함수 문장(선언문, statement)와 표현식(expression)을 다르게 인식

  ```javascript
  function func1(x: number): number {(...)} // statement
  const func2 = function(x: number): number {(...)} // expression
  const func3 = (x: number): number => {(...)} // expression
  ```

  - 표현식은 매개 변수&반환값 전체 함수타입 선언 가능 => 재사용 가능

  ```javascript
  // 함수 타입 전체를 타입으로 선언
  type FuncType = (x: number, y: number) => number;
  const rollDice: FuncType = (sides) => 0;

  // 추가적인 재사용도 가능
  const add: FuncType = (a, b) => a + b;
  const sub: FuncType = (a, b) => a - b;
  ```

  - 라이브러리는 공통 함수 시그니처를 타입으로 제공하기도 함
    - MouseEvent: 함수의 매개변수에 명시하는 타입
    - MouseEventHandler: 함수 전체에 적용할 수 있는 타입
    - 함수 시그니처: 함수의 타입을 지칭

### **2. 다른 함수의 시그니처 참조는 'typeof fn'으로 가능**

```javascript
// 내장함수 fetch의 타입을 가져와 쓰는 모습
const checkedFetch: typeof fetch = async (input, init) => {
  const response = await fetch(input, init);
  if (!response.ok) {
    throw new Error("Request failed: " + response.status);
  }
  return response;
};
```
