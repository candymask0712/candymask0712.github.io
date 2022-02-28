---
title: "[TypeScript] 배열 안에 들어 있는 객체 다루기 (feat. String literal)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - String literal
  - Comong
last_modified_at:
---

### **1. 배열 안에 있는 객체 다루기**

오늘 4주 프로젝트를 하면서 API로 장바구니 데이터를 받았다  
데이터는 배열 안에 객체가 들어 있는 형식이이었는데 처음 다루는데 어려움을 겪어 기록으로 남기려고 한다

먼저 Redux Toolkit을 이용해 받아온 데이터를 for...in 문으로 순회하고 출력해보았다

```javascript
// cart.tsx
let data = cartData.cartSlice.data[0];
console.log("data", data);
for (let x in data) {
  console.log("x", x);
}
```

아래와 같이 잘 출력되는 것을 볼 수 있다

![image](https://user-images.githubusercontent.com/86667412/154780631-54deee35-4634-414a-a107-6a6c3dee2b75.png)

그러나 개별 키에 해당하는 값에 접근하려고 하면 문제가 발생한다

```javascript
// cart.tsx

let data = cartData.cartSlice.data[0];
console.log("data", data);
for (let x in data) {
  console.log(x, data[x]);
}
```

`'string' 형식의 식을 '{}' 인덱스 형식에 사용할 수 없으므로 요소에 암시적으로 'any' 형식이 있습니다. '{}' 형식에서 'string' 형식의 매개 변수가 포함된 인덱스 시그니처를 찾을 수 없습니다.`  
![image](https://user-images.githubusercontent.com/86667412/154780774-9d6b632d-5034-47f8-a7e6-d7ce17cf9b5d.png)
![image](https://user-images.githubusercontent.com/86667412/154780745-327bcbd3-7fa6-4fef-8696-7a7daa444c92.png)

검색을 통해 index signature와 string literal에 대해 알게 되었다
아래와 같이 index의 형식을 지정해 주면 에러는 쉽게 해결할 수 있다

```javascript
// cartSlice.tsx

export interface Cart {
  data: { [index: string]: string }[];
}
```

원인은 string literal만 허용되는 곳에 string타입을 사용했기 때문이다
string literal은 string보다 더 좁은(narowed) 타입이기 때문에 오타 등으로 유효하지 않은 이름으로 인한 런타임을 에러를 방지하는데 도움이 된다고 한다

참고한 블로그 글의 서두에
`TS는 JS의 관점에서 벗어나지 못한 상태로 보았을 때 매우 이상하게 느껴질 때가 있다`
는 부분이 크게 공감 되었다

이번에 프로젝트를 TS로 진행하는 것을 계기로 TS에 대해 더 많은 공부를 해야겠다

### 2. 요약

- String타입의 키로 객체에 접근하려면 index signature를 선언해야 한다
