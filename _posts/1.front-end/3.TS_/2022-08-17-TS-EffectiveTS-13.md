---
title: "[TypeScript] Effective TS - item.13 타입과 인터페이스의 차이점 "
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

### **1. 타입과 인터페이스의 비슷한 점**

- 명명된 타입(named type)사용시 대부분 타입, 인터페이스 모두 사용 가능
- 잉여 속성 체크, 인덱스 시그니처, 함수 타입 정의, 제너릭 가능

  ```javascript
  // 인덱스 시그니처
  type TDict = {
    [key: string]: string
  };
  interface IDict {
    [key: string]: string
  };

  // 함수 타입 정의
  type TFn = {
     (x: number) => string
  }
  interface IFn {
    // 파라미터 부분을 ()로 감쌈
    (x: number): string
  }
  const toStrT: TFn = x => '' + x // OK
  const toStrI: IFn = x => '' + x // OK

  // 제너릭
  // 제너릭 - 타입을 함수의 파라미터처럼 인자로 받아 사용하는 것
  type TPair<T> = {
    first: T
    second: T
  }
  interface IPair<T> {
    first: T
    second: T
  }

  // 타입 확장
  type TState = {
    name: string
    capital: string
  }
  interface IState {
    name: string
    capital: string
  }
  // IStateWithPop과 TStateWithPop은 동일
  interface IStateWithPop extends TState {
    population: number
  }
  type TStateWithPop = IState & { population: number }
  ```

### **2. 타입과 인터페이스의 다른 점**

- 유니온 타입은 있지만 유니온 인터페이스는 없음
  ```javascript
  type AorB = "a" | "b";
  ```
- 아래 타입은 인터페이스로는 표현 불가능
  ```javascript
  type NamedVariable = (Input | Output) & { name: string };
  ```
- 튜플, 배열 타입도 타입 키워드로 간결하게 구현 가능
  ```javascript
  // 타입 키워드로 선언시 튜플 간결하게 표현 가능
  type Pair = [number, number]
  type StringList = string[]
  type NamedNums = [string, ...number[]]

  // 인터페이스로도 튜플 비슷하게 구현 가능
  interface Tuple {
    0: number
    1: number
    length: 2
  }
  const t: Tuple = [10, 20] // OK
  t.concat(t) // error
  ```
- 인터페이스는 보강(선언 병합)이 가능
- 주로 타입 선언 파일에서 사용되며 TS 내부에서도 ES스펙 정의에 보강 사용
  ```javascript
  interface IState {
    name: string
  }
  interface IState {
    population: number
  }
  const wyoming: IState = {
    name: 'Wyoming',
    population: 500_000,
  } // OK
  ```

