---
title: "[JavaScript] 숫자, 문자열 다루기"
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JavaScript
tags:
  - slice
  - parseInt
  - type
last_modified_at:
---

### 1. **Math.floor와 parseInt의 차이**

Math.floor() 는 내림한다.  
parseInt() 는 소수점 아래를 그냥 버린다.

- 양수일 경우 (동일)

```javascript
a = Math.floor("1.34"); // 1
b = Math.floor("3.98"); // 3

a2 = parseInt("1.34"); // 1
b2 = parseInt("3.98"); // 3
```

- 음수일 경우 (Math.floor는 앞자리 변동)

```javascript
c = Math.floor("-1.34"); // -2
d = Math.floor("-5.69"); // -6

c2 = parseInt("-1.34"); // -1
d2 = parseInt("-5.69"); // -5
```

- 그 외 (여러 수 입력시)

```javascript
Math.floor("12  34  56"); // NaN

parseInt("12  34  56"); // 12
```

### 2. **slice의 인수 생략 시 출력**

slice() 메소드는 원본 배열은 수정되지 않는다.

#### 1) start: 추출 시작점에 대한 인덱스 (이상)

undefined인 경우: 0부터 slice
음수를 지정한 경우: 배열의 끝에서부터의 길이를 나타낸다. slice(-2)를 하면 배열의 마지막 2개의 요소를 추출한다.
배열의 길이와 같거나 큰 수를 지정한 경우: 빈 배열을 반환한다.

#### 2) end: 추출을 종료할 기준 인덱스 (미만)

지정하지 않을 경우: 배열의 끝까지 slice
음수를 지정한 경우: 배열의 끝에서부터의 길이를 나타낸다. slice(2, -1)를 하면 세번째부터 끝에서 두번째 요소까지 추출
배열의 길이와 같거나 큰 수를 지정한 경우: 배열의 끝까지 추출.

반환값: 추출한 요소를 포함한 새로운 배열.

```javascript
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = arr.slice(3, 5); // [4, 5]
var arr2 = arr.slice(undefined, 5); // [1, 2, 3, 4, 5]
var arr3 = arr.slice(-3); // [8, 9, 10]
var arr4 = arr.slice(-3, 9); // [8, 9]
var arr5 = arr.slice(10); // []
var arr6 = arr.slice(4); // [5, 6, 7, 8, 9, 10]
var arr7 = arr.slice(undefined); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var arr8 = arr.slice(5, -4); // [6]
var arr9 = arr.slice(2, 15); // [3, 4, 5, 6, 7, 8, 9, 10]
```
