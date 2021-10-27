---
title: "[JS] 고차함수의 이해  "
excerpt: "21년 10월 29일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - higher order function
  - JS
  - TIL
last_modified_at:
---

### **1. 함수와 일급객체의 특징**
  - 함수는 JS의 일급객체(first-class)
  - 따라서 아래와 같은 특징을 가진다
    - 변수에 할당할 수 있다
    - 다른 함수의 인자로 전달될 수 있다
    - 다른 함수의 결과로 리턴될 수 있다
    - 
### **2. 고차함수(higher order function)란?**
  - 함수를 인자로 받을 수 있고 함수의 형태로 리턴할 수 있는 함수
  - 콜백 함수(callback): 다른 함수(caller)의 인자로 전달되는 함수
  - 커리함수: 함수를 리턴하는 함수   
    -> 이 경우 고차함수는 함수를 인자로 받는 함수로 한정하기도 함

1. 다른 함수를 인자로 받는 경우
```javascript
function double(num) {
  return num * 2;
}

function doubleNum(func, num) {
  return func(num);
}

/*
 * 함수 doubleNum은 다른 함수를 인자로 받는 고차 함수입니다.
 * 함수 doubleNum의 첫 번째 인자 func에 함수가 들어올 경우
 * 함수 func는 함수 doubleNum의 콜백 함수입니다.
 * 아래와 같은 경우, 함수 double은 함수 doubleNum의 콜백 함수입니다.
 */
let output = doubleNum(double, 4);
console.log(output); // -> 8
```

2. 함수를 리턴하는 경우
```javascript
function adder(added) {
  return function (num) {
    return num + added;
  };
}

/*
 * 함수 adder는 다른 함수를 리턴하는 고차 함수입니다.
 * adder는 인자 한 개를 입력받아서 함수(익명 함수)를 리턴합니다.
 * 리턴되는 익명 함수는 인자 한 개를 받아서 added와 더한 값을 리턴합니다.
 */

// adder(5)는 함수이므로 함수 호출 연산자 '()'를 사용할 수 있습니다.
let output = adder(5)(3); // -> 8
console.log(output); // -> 8

// adder가 리턴하는 함수를 변수에 저장할 수 있습니다.
// javascript에서 함수는 일급 객체이기 때문입니다.
const add3 = adder(3);
output = add3(2);
console.log(output); // -> 5
```

3. 함수를 인자로 받고, 함수를 리턴하는 경우
```javascript
function double(num) {
  return num * 2;
}

function doubleAdder(added, func) {
  const doubled = func(added);
  return function (num) {
    return num + doubled;
  };
}

/*
 * 함수 doubleAdder는 고차 함수입니다.
 * 함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백 함수입니다.
 * 함수 double은 함수 doubleAdder의 콜백으로 전달되었습니다.
 */

// doubleAdder(5, double)는 함수이므로 함수 호출 기호 '()'를 사용할 수 있습니다.
doubleAdder(5, double)(3); // -> 13

// doubleAdder가 리턴하는 함수를 변수에 저장할 수 있습니다. (일급 객체)
const addTwice3 = doubleAdder(3, double);
addTwice3(2); // --> 8
```



### **2.**

1. 


Achievement Goals
일급 객체(first-class citizen)의 세 가지 특징을 설명할 수 있다.
고차 함수(higher-order function)에 대해 설명할 수 있다.
고차 함수를 자바스크립트로 작성할 수 있다.
Advanced Challenges
더 생각해 볼 주제에 대해서 공부하고, TIL을 작성할 수 있다.

```javascript
```
`<code>` 코드강조

[링크명](링크주소)    
![대체텍스트](이미지주소)

*** 
수평선

>인용
>>인용2

| | |
---|---
| | |
| | |

| | |
---|---
| 
|

<small></small>