---
title: "[JS] Spread/Rest, Destructing 문법 "
excerpt: "21년 10월 28일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - JS
  - TIL
last_modified_at:
---

### **1.Spread 문법**
  - 배열을 풀어서 인자/요소로 넣을 때 사용
  - `...` 문자를 사용해서 배열의 요소 전개

  1. 배열 합치기
   
```javascript
let arr1 = ['A', 'B'];
let arr2 = ['C', ...parts, 'D', 'F'];
console.log(arr2);
// ['C', 'A', 'B', 'D', 'F']
// spread 문법은 기존 배열을 변경하지 않음
```

```javascript
let arr1 = [1, 2, 3];
let arr2 = [...arr]; // arr.slice() 와 유사
arr2.push(4);
console.log(arr1); // [1, 2, 3]
console.log(arr2); // [1, 2, 3, 4]
```

  2. 객체에서 사용하기
```javascript
let obj1 = { foo: 'bar', x: 42 };
let obj2 = { foo: 'baz', y: 13 };

let clonedObj = { ...obj1 };
// {foo: 'bar', x: 42}
let mergedObj = { ...obj1, ...obj2 };
// {foo: 'baz', x: 42, y: 13}

// 키가 중복이면 나중값으로 덮어씌워짐
```
  
### **2.rest 문법**
  - 파라미터를 배열의 형태로 받아 사용
  - 파라미터의 개수가 가변적일 때 유용
```javascript
function sum(...theArgs) {
  return theArgs.reduce((previous, current) => {
    return previous + current;
  });
}

sum(1,2,3) // 6
sum(1,2,3,4) // 10
```

### **3.Destructing(구조 분해)**
  - spread 문법을 이용 값 해체   
  -> 개별 값을 변수에 새롭게 할당  

```javascript
const [a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30,40,50]
```

```javascript
const {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40}
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c:30, d:40}

const {e, f, ...rest} = {a: 10, b: 20, c: 30, d: 40}
console.log(e); // undefined
console.log(f); // undefined
console.log(rest); // {a: 10, b: 20, c: 30, d: 40}
// 선언한 변수명과 키값이 일치하지 않으면 불가
// 나머지 전부가 rest에 할당 됨

const {e, f, ...leftover} = {a: 10, b: 20, c: 30, d: 40}
console.log(e); // undefined
console.log(f); // undefined
console.log(leftover); // {a: 10, b: 20, c: 30, d: 40}

// rest에 해당하는 변수명은 작명 가능
```

- 객체에서의 shorthand(단축문법)
```javascript
  it('객체의 단축(shorthand) 문법을 익힙니다', () => {
    const name = '김코딩'
    const age = 28

    const person = {
      name,
      age,
      level: 'Junior',
    }
    console.log(person);
    // {  
    //   name: '김코딩',
    //   age: 28,
    //   level: 'Junior',
    // }
    
    // 객체 내 변수명만 기재 시
    // 변수명을 키, 변수의 값을 값으로 가짐
```




### **4.swallow copy & deep copy**  
  - swallow copy : 참조자료형, 주소를 복사
  -> 메모리 구조상 heap에 저장해 효율성 확보 목적

    - Object.assign은 첫번째 요소로 들어온 객체에 다음인자로 들어온 객체를 복사해준다
    ```javascript
      const obj = {
        a: 1,
        b: {
          c: 2,
        },
      };

      const copiedObj = Object.assign({}, obj);

      copiedObj.b.c = 3

      obj === copiedObj // false
      obj.b.c === copiedObj.b.c // true
    ```

  - deep copy : 원시자료형, 값 자체를 복사
      -> 크기가 크지않아 stack에 저장 가능
    ```javascript
    let A = {...obj}
    let B = [...arr]
    let C = arr.slice()
    let D = arr.slice(0)
    // 배열, 객체를 deep copy 하고 싶을 때
    ```