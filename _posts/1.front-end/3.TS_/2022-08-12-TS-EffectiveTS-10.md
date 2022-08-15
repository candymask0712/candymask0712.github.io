---
title: "[TypeScript] Effective TS - item.10 - 객체 레퍼 타입 피하기"
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

### **1. 기본형 값에 메서드 제공 위해 객체 래퍼 타입 이해 필요**

- JS 7가지 기본형 값은 불변, 메서드 x
- 기본형 메서드 사용 시 객체로 래핑(wrap) 후 사용 -> 호출 -> 객체 제거

```javascript
// 기본형 값은 소문자, 객체 래퍼 타입은 대문자로 시작
// null, undefined 제외 모두 객체 레퍼 타입 존재
string - 기본형 값
String - 객체 래퍼 타입

// 몽키패치 예시(런타임 기능수정 - JS에서는 주로 프로토타입 변경)
// 객체 래퍼 타입의 동작을 알기위한 코드(이런 코드 작성하면 안됨)
const originalCharAt = String.prototype.charAt
String.prototype.charAt = function (pos) {
  // 여기서의 this는 String 객체 래퍼
  console.log(this, typeof this, pos) // [String: 'primitive'] 'object' 3
  return originalCharAt.call(this, pos)
}
console.log('primitive'.charAt(3)) // let answer=Number.MAX_SAFE_INTEGER;
```

- 객체 래퍼 타입은 기본형과 비슷하게 동작하나 차이점 존재
- 자기 자신과만 동일하고 속성을 기본형에 할당 시 속성이 사라짐

### **2. TS 객체 래퍼 타입은 지양하고 기본형 타입 사용 필요**

- TS는 기본형과 객체 레퍼 타입을 별도로 모델링
- 객체 래퍼 사용 하지 않도록 주의 (처음 잘 동작하는 것처럼 보일 수 있음)

```javascript
// 기본형 string 대신 객체 레퍼 타입 String을 사용했으나 잘 동작
const getStringLen = (foo: String) => foo.length;

getStringLen("hello"); // OK
getStringLen(new String("hello")); // OK
```

```javascript
// error: String 형식의 인수를 string 형식의 매개 변수에 할당 불가
const isGreeting = (phrase: String) => ["hello", "good day"].includes(phrase);
```
