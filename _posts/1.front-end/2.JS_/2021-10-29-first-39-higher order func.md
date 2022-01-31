---
title: "[JavaScript] 일급 객체와 주요 고차함수 "
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JavaScript
tags:
  - higher order function
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


   // 함수 doubleNum은 다른 함수를 인자로 받는 고차 함수입니다.
   // 함수 doubleNum의 첫 번째 인자 func에 함수가 들어올 경우
   // 함수 func는 함수 doubleNum의 콜백 함수입니다.
   // 아래와 같은 경우, 함수 double은 함수 doubleNum의 콜백 함수입니다

  let output = doubleNum(double, 4);
  console.log(output); // -> 8
  ```

1. 함수를 리턴하는 경우

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

1. 함수를 인자로 받고, 함수를 리턴하는 경우

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

// 함수 doubleAdder는 고차 함수입니다.
// 함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백 함수입니다.
// 함수 double은 함수 doubleAdder의 콜백으로 전달되었습니다.

// doubleAdder(5, double)는 함수이므로 함수 호출 기호 '()'를 사용할 수 있습니다.
doubleAdder(5, double)(3); // -> 13

// doubleAdder가 리턴하는 함수를 변수에 저장할 수 있습니다. (일급 객체)
const addTwice3 = doubleAdder(3, double);
addTwice3(2); // --> 8
```

### **3. 고차함수를 사용해야 하는 이유**
- 순수함수를 통해 부수효과를 억제하여 프로그램에 안정성 높임

### **4. 주요 고차함수**

|원본 배열 변경 |원본 배열 미변경 |
---|---
|sort|forEach, map, filter, reduce|


1. sort
    - 배열의 요소를 변경

    ```javascript
    배열.sort();
    // 원본배열을 정렬 (오름차순- 유니코드 기준)
    배열.sort().reverse;
    // 내림차순 원할 시 reverse 매서드와 조합
    배열.sort((a-b)=> a-b); // 숫자 오름차순
    // 유니코드는 문자열 기준임 따라서
    // 숫자정렬 시 비교함수를 인자로 전달해야 함
    ```

2. forEach
 
3. filter

    ```javascript
    배열.filter((요소, 인덱스, 배열) => { return 요소 });
    // 콜백함수의 반환값이 true인 요소로만 이루어진 새 배열 반환
    ```

4. map

    ```javascript
    배열.map((요소, 인덱스, 배열) => { return 요소 });
        // 콜백함수의 반환값으로 이루어진 새 배열을 반환
    ```

5. reduce

    ```javascript
    배열.reduce((누적값, 현잿값, 인덱스, 요소) => { return 결과 }, 초깃값);
    // 콜백함수의 반환값으로 이루어진 새 배열을 반환
    // return 값을 누적값에 업데이트하여 하나의 값을 출력
    배열.reduce((누적값, 현잿값) => { 
      if(조건 1) return 누적값;
      // 조건1의 경우 return에 누적값만 있어 변화 없음
      else if(조건 2) return 누적값 + 현재값
      }, 초깃값);
    ```
