---
title: "[TypeScript] Effective TS - item.01 - TS와 JS의 관계 이해하기"
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

### **1. JS는 TS의 부분 집합**

```javascript
// 타입이 추가 된 아래 코드는 JS 런타임에서 에러 발생
function func(x: string) {
  console.log(x);
}
```

### **2. TS는 JS의 런타임 동작을 모델링**

- TS는 초기값으로부터 타입을 추론

  ```javascript
  // x의 초기값 'a'에서 string 타입을 추론
  const x = "a";

  // 아래 코드는 '...is not a function' 에러 발생
  // 추론한 string에 toUppercase 속성이 없음을 알림
  console.log(x.toUppercase());
  ```

### **3. TS는 JS보다 문법 체크가 엄격함**

- TS는 JS보다 엄격한 문법 체크를 통해 오류를 예방

  ```javascript
  // 아래 코드는 JS에서는 모두 정상 작동
  // TS에서는 각각 '+ 연산자를 적용할 수 없음', '0~1개의 인수가 필요함' 표시
  const a = null + 7;
  const b = [] + 12;
  alert("x", "y");
  ```

- 위와 같이 JS에서 작동은 되지만 이상한 코드를 쓰는 것을 방지
- 아래 링크는 JS 이상한 코드를 모은 링크입니다  
  (아래 링크 내 내용을 TS에서 모두 방지해준다는 것은 아님!)  
  [JS is Weird 퀴즈](https://velog.io/@jungsangu/JS-Is-Weird)  
  [JS로 'banana' 출력하기](https://m.blog.naver.com/dlaxodud2388/222189731481)  
  [WTF JS](https://github.com/denysdovhan/wtfjs)
