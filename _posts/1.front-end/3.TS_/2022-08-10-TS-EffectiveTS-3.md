---
title: "[TypeScript] Effective TS - item.03 - 코드 생성과 타입 체크는 무관"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - Effective TS
  - tsconfig
last_modified_at:
---

### **1. TS 컴파일러의 두 가지 역할**

- 호환성을 위해 최신 TS/JS를 구버전의 JS로 트랜스파일
- TS 코드의 타입 오류를 체크
- 두 역할은 서로 독립적으로 작동

### **2. 타입 오류가 있어도 컴파일 가능**

- 타입 오류가 있어도 컴파일 된 산출물이 있는 것이 다른 부분 확인에 도움됨
- 오류 존재 시 컴파일 하지 않는 옵션 있음(noEmitOnError)

### **3. 런타임에는 타입 체크가 불가능**

- 아래 4가지 예시를 통해 런타임에서의 타입 체크 이해
- interface인 Square와 Rectangle을 구분하는 사례

- 타입 관련 코드는 컴파일 시 제거 되 체크가 불가능

  ```JavaScript
  // 타입 관련 내용은 컴파일 시 제거 됨 (interface, type 등)
  // (= 컴파일 된 JS 파일에는 존재하지 않게 됨)
  interface Square {
    width: number
  }
  interface Rectangle extends Square {
    height: number
  }
  type Shape = Square | Rectangle

  function calculateArea(shape: Shape) {
    // interface인 조건문의 Rectangle은 제거 되어 비교 불가
    if (shape instanceof Rectangle) {
      (...)
    }
  }
  ```

- 만약 위 예시에서 타입 확인을 하고 싶다면 속성을 확인해야함

  ```JavaScript
  (...)
  function calculateArea(shape: Shape) {
    // 해당 객체에 height라는 속성이 있는지 직접 확인
    if ('height' in shape) {
      (...)
    }
  }
  ```

- 런타임에 접근가능한 타입 정보를 저장하는 '태그' 기법

  ```JavaScript
  interface Square {
    kind: 'square'
    (...)
  }
  interface Rectangle extends Square {
    kind: 'rectangle'
    (...)
  }
  type Shape = Square | Rectangle

  function calculateArea(shape: Shape) {
    // 명시적으로 타입 정보를 저장하는 kind 속성을 통해 구분
    if (shape.kind === 'rectangle') {
      (...)
    }
  }
  ```

  - 태그된 유니온을 다른 표현으로 '서로소 유니온'으로도 부르고 있네요
  - 저에게는 의미도 잘 와닿고 좀 더 설명히 상세하여 첨부합니다
    [서로소 유니온 타입](https://ahnheejong.gitbook.io/ts-for-jsdev/06-type-system-deepdive/disjoint-union-type)

- 타입 연산은 런타임에 영향을 주지 않음

### **3. 타입 연산은 런타임에 영향을 주지 않음**

```JavaScript
// (TS 코드)
// Type Assertion 으로 반환되는 val의 타입을 숫자로 강제함
// Type Assertion 설명 링크: https://radlohead.gitbook.io/typescript-deep-dive/type-system/type-assertion
function asNumber(val: number | string): number {
  return val as number
}

// (JS 코드 - 트랜스파일링 됨)
// 타입 코드 제거 됨 => 타입과 무관하게 val 반환
function asNumber(val) {
  return val
}

// (TS 코드 - 의도에 맞게 수정 됨)
function asNumber(val: number | string): number {
  return Number(val)
}
```

### **4. 런타임 타입은 선언 타입과 다를 수 있음**

```JavaScript
// 아래 함수는 파라미터가 boolean으로 들어옴
// TS 자체로는 default 케이스로 넘어가는 경우가 없음
function threeCase(value: boolean) {
  switch (value) {
    case true:
      console.log('case: true')
      break
    case false:
      console.log('case: false')
      break
    default:
      console.log('case: default')
  }
}

// 그러나 API 요청의 응답이 boolean이 아닐 경우
// 예외적으로 default 케이스로 넘어갈 수도 있음
interface ApiResponse {
  value: boolean
}
async function apiCode() {
  const response = await fetch('/case')
  const result: ApiResponse = await response.json()
  threeCase(result.value)
}
```

### **5. TS의 타입으로는 함수 오버로드 불가**

- TS의 함수 오버로딩은 타입 수준에서만 작동
- TS에서는 하나의 함수에 하나의 구현체만 허용 (타입 선언은 여러개 가능)
- 함수 오버로딩: 매개변수만 다른 여러 버젼의 함수 사용

```JavaScript
// TS설정: {"noImplicitAny":false}

// 아래 두 줄은 컴파일 시에는 제거 됨
function add(a: number, b: number): number
function add(a: string, b: string): string

function add(a, b) {
  return a + b
}

const three = add(1, 2) // Type is number
const twelve = add('1', '2') // Type is string
```

### **5. TS의 타입은 런타임 성능에 영향 없음**

- 타입 코드는 트랜스파일링시 제거 => 성능과 무관
- TS의 컴파일 속도는 상당히 빠른 편
- 오버헤드가 커질 시 타입체크를 생략하고 트랜스파일만 하는 옵션도 존재
- 오버헤드: 어떤 처리에 드는 간접적 시간 및 메모리
