---
title: "[javascript] event loop란 무엇인가"
excerpt: "21년 11월 18일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - event loop
  - JS
  - TIL
last_modified_at:
---

[참고자료 - 어쨌든 이벤트 루프는 무엇입니까?](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=608s)

### **1. 이벤트루프**

1. javascript의 콜스택

   - 자바스크립트는 싱글스레드 기반의 언어 -> 하나의 콜스택을 가짐
   - 콜스택은 먼저 main() 함수를 실행하고 작업을 순차적으로 쌓음 -> 맨 위 것만 실행
   - 콜스택에 너무 많은 내용이 쌓이면 스택 오버플로우 발생

2. javascript에서의 블로킹

   - 동기적으로 실행되는 네트워크 요청이 있다면 콜스택을 블로킹
   - 다른 작업이나 랜더링 불가능

3. javascript와 web API

   - setTimeout은 V8 소스코드에는 없음
   - javascript가 실행되는 런타임 환경에 존재하는 API
   - 웬브라우져에서 제공하는 web API가 동시성을 지원

4. 이벤트루프

   - 스택과 테스크큐를 주시하면서 작업을 처리
   - 스택이 비어있고 테스크 큐에 작업이 있다면 스택으로 이동시켜줌
   - 따라서 setTimeout 정확한 시간이 아니라 API에서 딜레이 될 시간만 정할 수 있음

5. 랜더큐

   - javascript는 60분의 1초마다 랜더링을 하나 스택이 깨끗할 때만 랜더링 진행
   - 랜더 큐에서 콜스택이 깨끗한지 확인 후 랜더링 진행
   - 만약 랜더링이 불가능할 경우 우리가 웹에서 하는 동작이 작동하지 않음
   - 스택에 불필요한 동작이 있어 스택을 막아서는 안됨!

```javascript

```

- 내용

```javascript

```

### **1. 소제목**

1. 넘버링

- 내용

```javascript

```

- 내용

```javascript

```

```javascript

```

`<code>` 코드강조

[링크명](링크주소)  
![대체텍스트](이미지주소)

---

수평선

> 인용
>
> > 인용2

|     |     |
| --- | --- |
|     |     |
|     |     |

|     |     |
| --- | --- |

|
|

<small></small>
