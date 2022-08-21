---
title: "[TypeScript] Effective TS - item.11 잉여 속성 체크의 한계 인지"
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

### **1. 잉여 속성 체크와 구조적 할당 가능성 체크 구분 필요**

- '객체 리터럴'을 할당, 매개변수 전달시에만 잉여 속성 체크 수행

```javascript
interface Room {
  numDoors: number
  ceilingHeightFt: number
}
// 예시 1) 직접 객체 리터럴 할당 - 잉여 속성 체크 O
const r: Room = {
  numDoors: 1,
  ceilingHeightFt: 10,
  // error: 객체 리터럴은 알려진 속성만 지정할 수 있음
  // Room 형식에 elephant 없음
  elephant: 'present',
}

// 예시 2) 임시 객체 생성 후 할당 - 잉여 속성 체크 X
const obj = {
  numDoors: 1,
  ceilingHeightFt: 10,
  elephant: 'present',
}
const r: Room = obj // OK
```

- TS는 의도와 다르게 작성 된 코드도 찾으려 함

  ```javascript
  // 아래 코드 실행 시 런타임에서 오류 발생 x
  // 그러나 의도와는 다른 동작일 수 있음 오류 메세지 안내
  interface Options {
    title: string
    darkMode?: boolean
  }
  function createWindow(options: Options) {
    if (options.darkMode) {
      setDarkMode()
    }
    // ...
  }
  createWindow({
    title: 'Spider Solitaire',
    // darkMode, darkmode 대소문자 차이 => 의도한 것인지 확인
    // darkmode으로 넣어도 darkMode가 없는 것으로 인식해 작동
    darkmode: true,
  })
  ```

- 잉여 속성 체크 원치 않을 시 인덱스 시그니처 사용
  ```javascript
  interface Options {
    darkMode?: boolean
    // key로는 string인 어떤 값, value로는 unknown 값 들어올 수 있음
    [otherOptions: string]: unknown
  }
  const o: Options = { darkmode: true } // OK
  ```
