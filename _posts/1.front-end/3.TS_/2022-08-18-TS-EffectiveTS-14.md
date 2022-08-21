---
title: "[TypeScript] Effective TS - item.14 타입 연산과 제너릭 사용으로 반복 줄이기"
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


## **1. DRY원칙을 타입에 적용하기**
- TS 사용시에는 공유된 패턴 제거가 익숙치 않아 중복이 더 흔함
- DRY(don't repeat yourself) 원칙을 타입에도 적용 필요

### **2. 타입 이름과 extends 사용하기**
- 반복 되는 타입에 이름을 붙여 공통화하기
- 공통 필드를 가진 인터페이스는 확장 사용하기
  ```javascript
  interface Person {
    firstName: string
    lastName: string
  }

  // extends 문법을 이용해 Person에 있는 필드 가져옴
  interface PersonWithBirthDate extends Person {
    birth: Date
  }
  //위 내용을 인터섹션 연산자(&)로도 표현 가능 (유니온 타입에서 유용)
  type PersonWithBirthDate = Person & { birth: Date}
  ```

### **3. 타입 간 매핑을 위해 TS가 제공하는 도구 사용**

- 매핑 된 타입 사용 시 중복 제거가 용이
  ```javascript

  // 상위집합 State와 하위집합 TopNavState
  interface State {
    userId: string
    pageTitle: string
    recentFiles: string[]
    pageContents: string
  }

  interface TopNavState {
    userId: string
    pageTitle: string
    recentFiles: string[]
  }

  // 아래와 같이 수정 시 State 수정 사항이 반영 됨
  type TopNavState = {
    userId: State['userId']
    pageTitle: State['pageTitle']
    recentFiles: State['recentFiles']
  }

  // '매핑된 타입' 사용 시 반복되는 부분을 간결하게 표현 가능 
  type TopNavState = {
    [k in 'userId' | 'pageTitle' | 'recentFiles']: State[k]
  }
  // 제너릭 타입 Pick 사용시 더 간결하게 표현 가능
  // Pick은 두 개의 타입을 받아 결과 타입을 반환 
  type TopNavState = Pick<State, 'userId' | 'pageTitle' | 'recentFiles'>
  type Pick<T, K> = { [k in K]: T[k] }
  ```

  ```javascript
  interface SaveAction {
    type: 'save'
    // ...
  }
  interface LoadAction {
    type: 'load'
    // ...
  }
  type Action = SaveAction | LoadAction
  type ActionType = 'save' | 'load' // Repeated types!
  type ActionType = Action['type'] // Type is "save" | "load"
  type ActionRec = Pick<Action, 'type'> // {type: "save" | "load"}
  ```

  ```javascript
  interface Options {
    width: number
    height: number
    color: string
  }
  // 클래스 내 옵션 업데이트를 위한 type
  // optional로 변경될 것을 대비 모두 ? 처리
  interface OptionsUpdate {
    width?: number
    height?: number
    color?: string
  }
  // 아래와 같이 순회하면서 ?를 붙이면 간결하게 표현 가능
  type OptionsUpdate = { [k in keyof Options]?: Options[k] }
  // 내장 함수 Partial 사용도 가능 (모든 타입 optional하게 만듬)
  type OptionsUpaate2 = Partial<Options>

  class UIWidget {
    constructor(init: Options) {
      /* ... */
    }
    update(options: OptionsUpdate) {
      /* ... */
    }
  }  
  ```

  - 값 또는 리턴 값으로 부터 타입을 얻는 방법
    ```javascript
    // (값에서 타입을 얻어내는 방법)
    const INIT_OPTIONS = {
      width: 640,
      height: 480,
      color: '#00FF00',
      label: 'VGA',
    }
    // 아래와 같이 별도로 타입 선언 시 중복(타입은 값 할당 시 추론 됨)
    interface Options {
      width: number
      height: number
      color: string
      label: string
    }
    // typof 사용 시 값에서 타입을 얻어낼 수 있음
    type Options = typeof INIT_OPTIONS

    // (리턴 값에서 타입을 얻어내는 방법)
    const INIT_OPTIONS = {
      width: 640,
      height: 480,
      color: '#00FF00',
      label: 'VGA',
    }
    function getUserInfo(userId: string) {
      // COMPRESS
      const name = 'Bob'
      const age = 12
      const height = 48
      const weight = 70
      const favoriteColor = 'blue'
      // END
      return {
        userId,
        name,
        age,
        height,
        weight,
        favoriteColor,
      }
    }
    
    // Return type inferred as { userId: string; name: string; age: number, ... }
    type UserInfo = ReturnType<typeof getUserInfo>
    ```
  - 제네릭을 통해 타입을 간결하게 표현 가능
  ```javascript
  interface Name {
    first: string
    last: string
  }
  type DancingDuo<T extends Name> = [T, T]
   
  const couple1: DancingDuo<Name> = [
    { first: 'Fred', last: 'Astaire' },
    { first: 'Ginger', last: 'Rogers' },
  ] // OK
  const couple2: DancingDuo<{ first: string }> = [
    // ~~~~~~~~~~~~~~~
    // Property 'last' is missing in type
    // '{ first: string; }' but required in type 'Name'
    { first: 'Sonny' },
    { first: 'Cher' },
  ]    
  ```
### **4. 타입을 위한 함수, 제너릭 사용하기**

