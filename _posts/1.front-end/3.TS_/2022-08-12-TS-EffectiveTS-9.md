---
title: "[TypeScript] Effective TS - item.09 - 타입 단언 보다는 타임 선언을 사용하기"
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

### **1. 타입 단언(as Type)보다 타입 선언(: Type)**

- 타입 단언은 TS가 추론한 타입을 무시하고 단언한 타입으로 강제 지정
- 안전성 체크가 가능한 '타입 선언'이 더 좋은 방식

  ```javascript
  interface Person {
    name: string
  }

  // 동일한 interface Person으로 지정 시
  // 타입 단언 방식은 필요한 속성이 없는 것을 체크하지 못함
  const alice: Person = {} // error (name 속성 없음)
  const bob = {} as Person // no error

  // 동일한 interface Person으로 지정 시
  // 타입 단언 방식은 없는 속성이 추가 된 것을 체크하지 못함
  const alice2: Person = {
    name: 'Alice',
    occupation: 'a',
  } // error (occupation 속정 존재)
  const bob2 = {
    name: 'Bob',
    occupation: 'b',
  } as Person // no error
  ```

  ### **2. 화살표 함수의 반환 타입을 명시하는 방법 숙지**

  - 화살표 함수의 타입 선언은 추론된 타입이 모호할 때가 있음
  - 정확한 반환 타입을 명시할 수 있어야 런타임 문제 예방 가능한

  ```javascript
  interface Person {
    name: string
  }
  // people의 type은 { name: string; }[]
  const people = ['alice', 'bob', 'jan'].map(name => ({ name }))

  // people2의 반환타입으로 인터페이스 Person을 적용하기위해 타입 단언 사용
  // 이 경우 people2을 가져다 사용할 다른 곳에서 런타임 시 문제 발생 가능성
  const people2 = ['alice', 'bob', 'jan'].map(name => ({ name } as Person)) // Type is Person[]

  // 책에서의 최종 해결책
  // (name): Person => name의 타입이 없고 반환 타입이 Person임을 명시
  // (name: Person) => name의 타입이 Person이고 반환타입이 없음 (오류 발생)
  const people3 = ['alice', 'bob', 'jan'].map((name): Person => ({ name }))

  // Roy가 제안하는 해결책
  // 변수 선언부에서 people의 형태를 지정해줌
  const people4: Person[] = ['alice', 'bob', 'jan'].map((name): Person => ({ name }))
  ```

  ### **3. TS보다 타입 정보를 잘 알고 있는 상황에서는 단언문 사용**

  - TS는 DOM 엘리먼트에 접근 불가 => 단언문 사용 타당

  ```javascript
  // tsConfig: {"strictNullChecks":false}
  document.querySelector('#myButton').addEventListener('click', e => {
    e.currentTarget // Type is EventTarget
    const button = e.currentTarget as HTMLButtonElement
    button // Type is HTMLButtonElement
  })
  ```

  - null이 아니라는 단언문을 사용해 명시도 가능 (접미사!)

  ```javascript
  const elNull = document.getElementById('foo') // Type is HTMLElement | null
  const el = document.getElementById('foo')! // Type is HTMLElement
  ```

  - 단언문으로 임의의 타입 간 변환은 불가능 (서브타입일 경우만 가능)
  - unknown이 포함 된 단언문은 항상 동작 (모든 타입은 unknown의 서브타입)

  ```javascript
  interface Person {
    name: string
  }
  // body와 Person은 충분히 overlap 되지 않다는 에러 발생
  const body = document.body
  const el = body as Person

  // unknown을 사용해 단언문을 적용
  const el2 = document.body as unknown as Person // OK

  // unknown 사용 시의 장점
  // 1. 명시적으로 무언가 위험한 동작이라는 점 알림
  // 2. a.propName 처럼 사용시 에러 발생 (any와의 차이점)
  export default {}
  ```
