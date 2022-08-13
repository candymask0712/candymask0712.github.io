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
  - Structural Typing
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

  [덕 타이핑과 구조적 타이핑](https://vallista.kr/%EB%8D%95-%ED%83%80%EC%9D%B4%ED%95%91%EA%B3%BC-%EA%B5%AC%EC%A1%B0%EC%A0%81-%ED%83%80%EC%9D%B4%ED%95%91/)

### **2. 클래스의 경우도 구조적 타이핑을 따름**

- 클래스에 타입을 넣어 쓰는 경우에도 구조적 타이핑을 따름

```javascript
// 클래스 C (foo 변수와 method 메서드 가짐)
class C {
  foo: string;
  constructor(foo: string) {
    this.foo = foo;
  }
  method() {}
}
// 생성자 함수를 통해 인스턴스 c 생성
// foo의 값으로 'instance of C'가 들어간 인스턴스
const c = new C("instance of C");

// 타입 C를 따르는 객체 d를 생성
// error. 'method' 속성이 '{ foo: string; }' 형식에 없지만 'C' 형식에서 필수입니다.
const d: C = { foo: "object literal" };

// 타입 C를 따르는 객체 e를 생성
// foo, method 속성이 모두 있으면 okay.
const e: C = { foo: "", method() {} };

class E {
  method() {}
}
class D extends E {
  foo: string;
  constructor(foo: string) {
    super();
    this.foo = foo;
  }
}
const f: C = new D(""); // prototype chain 상에 method가 존재하면 okay.

const g = Object.create({ method() {} }, { foo: { value: "" } }); // g: any
const h: C = g; // C type 강제(assert)하여 okay.

const i: { foo: string, method: () => void } = Object.create(
  { method() {} },
  { foo: { value: "" } }
);
const j: C = i; // { foo, method } 타입을 강제하여 okay.
```

### **3. 구조적 타이핑은 유닛 테스트 시에도 유용**

- 클래스에 타입을 넣어 쓰는 경우에도 구조적 타이핑을 따름

  ```javascript

  // PostresDB의 interface를 상정
  interface PostgresDB {
    runQuery: (sql: string) => any[]
  }
  interface Author {
    first: string
    last: string
  }
  // DB와는 별개의 인터페이스
  interface DB {
    runQuery: (sql: string) => any[]
  }
  // 테스트 시 DB의 인터페이스가 아니더라도 적용 가능
  function getAuthors(database: DB): Author[] {
    const authorRows = database.runQuery(`SELECT FIRST, LAST FROM AUTHORS`)
    return authorRows.map(row => ({ first: row[0], last: row[1] }))
  }
  ```
