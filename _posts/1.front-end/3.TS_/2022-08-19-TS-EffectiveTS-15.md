---
title: "[TypeScript] Effective TS - item.15 동적 데이터에 인덱스 시그니처 사용"
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


### **1. 런타임 때까지 속성을 알 수 없는 경우에만 인덱스 시그니처 사용**

- TS에서는 인덱스 시그니처 사용 유연하게 key-value 매핑 가능
- 타입 체크 시 4가지의 문제점이 발생
  ```javascript
  type Rocket = { [property: string]: string }
  // [문제점]
  // 1. 모든 키를 허용하여 잘못된 키도 포함 될 수 있음
  // 2. 특정키가 필요하지 않음 ({}도 허용)
  // 3. 속성마다 다른 타입을 가질 수 없음
  // 4. 자동완성 기능이 동작하지 않음
  const rocket: Rocket = {
    name: 'Falcon 9',
    variant: 'v1.0',
    thrust: '4,940 kN',
  } // OK
  ```
- 런타임 때까지 객체의 속성을 알 수 없는 경우에는 인덱스 시그니처 사용

  ```javascript
  // CSV 파일을 parsing 하기에 런타임 전 타입을 알 수 없는 상황
  // 데이터의 상황을 정확히 알 수 없을 때는 undefined 추가도 고려
  // 아래 함수의 리턴 값 사용시 undefined 여부를 체크해야 함
  function safeParseCSV(input: string): { [columnName: string]: string | undefined }[] {
    return parseCSV(input)
  }
  ```
### **3. 가능하면 인덱스 시그니처 보다 정확한 타입 사용**

- 가능한 필드가 제한되어 있다면 선택적 필드 or 유니온 타입 사용

  ```javascript
  interface Row1 {
    [column: string]: number
  } // 인덱스 시그니처 - 너무 광범위해서 부정확
  interface Row2 {
    a: number
    b?: number
    c?: number
    d?: number
  } // 선택적 필드 - 현실적으로 최선
  type Row3 =
    | { a: number }
    | { a: number; b: number }
    | { a: number; b: number; c: number }
    | { a: number; b: number; c: number; d: number }
  // 유니온 타입 - 가장 정확하지만 번거로움
  ```
- 인덱스 시그니처의 대안 Record or 매핑 된 타입
  ```javascript
  // [Record 사용 시]
  type Vec3D = Record<'x' | 'y' | 'z', number>
  // Type Vec3D = {
  //   x: number;
  //   y: number;
  //   z: number;
  // }
  type Record<K extends keyof any, T> = {
    [P in K]: T;
  };
  // [Record 미사용 시]
  type Vec3D = { [k in 'x' | 'y' | 'z']: number }
  // Same as above
  
  // [매핑된 타입 사용 시]
  // 키마다 별도의 타입 사용 가능
  type ABC = { [k in 'a' | 'b' | 'c']: k extends 'b' ? string : number }
  // Type ABC = {
  //   a: number;
  //   b: string;
  //   c: number;
  // }
  ```




