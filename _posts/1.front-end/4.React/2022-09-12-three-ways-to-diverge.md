---
title: "[React] React에서 분기처리 하는 법 4가지"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - Diverge
  - if



last_modified_at:
---

## **1. 가볍고 편한 상태관리 라이브러리 Zustand**



'리액트에서 자주쓰는 if문 작성패턴 5개'

## 1. 컴포넌트 안에서 쓰는 if/else

- 컴포넌트 return 부분(JSX)에서는 if문 사용 불가
- 분기에 따라 원하는 element 전체 return 필요
 
```javascript

// JSX에서의 분기 예시
function Component() {
  if ( true ) {
    return <p>참이면 보여줄 HTML</p>;
  } else {
    return null;
  }
} 

// return을 정확히 사용 시 else 생략 가능
function Component() {
  if ( true ) {
    return <p>참이면 보여줄 HTML</p>;
  } 
  return null;
} 
```

### 2. JSX안에서 쓰는 삼항연산자 

- 삼항 연산자(ternary operator)방식
  `조건문 ? 조건문 참일때 실행할 코드 : 거짓일 때 실행할 코드`
- JSX 안에서도 실행가능하며 (간단한 조건 시 유용)

  ```JavaScript
  function Component() {
    return (
      <div>
        {
          1 === 1
          ? <p>참이면 보여줄 HTML</p>
          : null
        }
      </div>
    )
  } 
  ```
 

3. && 연산자로 if 역할 대신하기

- &&(논리곱 연산자, 두 개의 앰퍼샌트를 사용)
- 참이면 '원하는 값' 아니라면 'null' 반환 시에 유용
 
  ```JavaScript
  function Component() {
    return (
      <div>
        {
          1 === 1
          ? <p>참이면 보여줄 HTML</p>
          : null
        }
      </div>
    )
  } 

  function Component() {
    return (
      <div>
        { 1 === 1 && <p>참이면 보여줄 HTML</p> }
      </div>
    )
  }
  ```

### 4. switch / case 조건문

- if문이 중첩해서 여러개 달려있는 경우에 사용
- 조건식란에서 변수하나만 검사할 수 있다는게 단점
 
  ```JavaScript
  // 일반적인 if문 사용시 다양한 분기 예시
  function Component2(){
    var user = 'seller';
    if (user === 'seller'){
      return <h4>판매자 로그인</h4>
    } else if (user === 'customer'){
      return <h4>구매자 로그인</h4>
    } else {
      return <h4>그냥 로그인</h4>
    }
  }
  // switch를 통해 개선한 모습
  function Component2(){
    var user = 'seller';
    switch (user){
      case 'seller' :
        return <h4>판매자 로그인</h4>
      case 'customer' :
        return <h4>구매자 로그인</h4>
      default : 
        return <h4>그냥 로그인</h4>
    }
  }
  // switch 사용법
  // 1. switch (검사할변수){} 작성
  // 2. 그 안에 case 비교대상 : 를 넣어줍니다.
  // 3. 그래서 이게 일치하면 case : 밑에 있는 코드를 실행
  // 4. default : 는 그냥 맨 마지막에 쓰는 else문과 동일
  ```

### 5. object/array 자료형 응용 

- 경우에 따라 다른 HTML을 보여주고 싶을 때 사용
- 삼항 연산자보다 더 많은 분기처리가 필요할 때 로직을 직관적으로 보여줌

  ```JavaScript
  var 탭UI = { 
    info : <p>상품정보</p>,
    shipping : <p>배송관련</p>,
    refund : <p>환불약관</p>
  }

  function Component() {
    var 현재상태 = 'info';
    return (
      <div>
        {
          탭UI[현재상태]
        }
      </div>
    )
  } 
  ```