---
title: "[javaScript] 스코프와 클로저"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JavaScript
tags:
  - closure
  - scope
last_modified_at:
---

### **1. 원시/참조 자료형**
  1. 원시 자료형(primitive type)  
    - 메모리 내 stack에 변수명과 값을 저장    
    - string, number, boolean, undefined 이 해당  
      a. null 은 원시 타입과 매우 비슷
         : 작동은 원시타입이나 타입은 객체    
           [참고자료 - Null(MDN)](https://developer.mozilla.org/en-US/docs/Glossary/Null)  
      b. bigint, symbol은 ES6에서 신규 도입  
    - 값 복사 후 원 데이터에는 영향 없음  

  2. 참조 자료형(reference type)   
    - 메모리 내 stack에 변수명과 heap 주소를 저장  
    - heap 주소지에는 자료의 원소들을 저장  
    - 효율성을 위해 동적으로 크기가 변하는 heap 이용
    - array, object, function 이 해당  
    - 값 복사 후 수정 시 원데이터도 수정 됨    
        a. 얕은 복사(swallow copy) : 주소 같음   
        b. 깊은 복사(deep copy) : 주소 다름

### **2. 스코프와 다양한 선언방식**

  1. 스코프(Scope)  
    - 스코프는 변수의 접근 범위  
    - 스코프는 global / local scope 로 나뉨  
    - local scope 는 block / function scope로 나뉨  
    - 변수는 스코프 내에서 선언된 것만 접근 가능 

      ||let |const |var|
      ---|---|---|---
      유효 스코프|블록/함수 |블록/함수 |함수
      값 재할당|가능 |불가능 |가능
      재선언|불가능 |불가능 |가능


```javascript
let x = 10;

function outF () {
  let x = 20;

  function inF () {
    x = x + 10;
    return x;
  }
  inF();
}

outF();
let answer = x;
// x = 10 , outF() 값이 연결된 곳 없음
```

```javascript
let x = 10;

function ouF () {
  x = 20;

  function inF () {
    let x
    x = x + 20;
    return x;
  }
  inF();
}

outF();
let result = x;
// x= 20, 역시 outF() 연결되어 있지 않으나
// outF() 안에서 x에 값이 할당 되면서 변화됨 
```
### **3. 클로저**

  1. 클로저의 정의
      - 함수와 함수가 선언 된 어휘적 환경의 조합(MDN)
      - 자신이 선언 된 환경을 기억 해 외부함수의 변수에 접근 가능한 내부 함수
      - 함수의 선언이 끝나고도 내부함수 변수 접근이 가능
      - 정보의 접근 제한 가능 (캡슐화)
        -> 재활용 가능한 함수를 제작 가능(모듈화)

```javascript
// 토글 버튼을 누르면 박스
var box = document.querySelector('.box');
var toggleBtn = document.querySelector('.toggle');

var toggle = (function () {
  var isShow = false;

  return function () {
    isShow = !isShow;
    box.style.display = isShow ? "block" : "none";
  };
})();

toggleBtn.onclick = toggle;
```