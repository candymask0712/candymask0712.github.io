---
title: "[React] React 기초 - 1 (React의 장단점과 JSX문법)"
excerpt: "React 기초"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - JavaScript
  - JSX
last_modified_at:
---

## React란

프론트앤드 개발을 위한 JS 오픈소스 라이브러리

### React의 장점

1. 선언형(Declarative) : JSX를 이용해 한 파일에 명시적으로 작성
2. 컴포넌트 기반(Component-Based) : 독립적/재사용 가능 -> 기능 자체에 집중한 개발 가능
3. 범용성(Learn Once, Write Anywhre) : JS 프로젝트에 유연하게 사용 가능

## JSX란

JS의 확장문법, Babel을 통해 JS로 컴파일 후 화면에 렌더링


## JSX의 기본문법

- 동적 인터페이스 구현을 위해서는 수 많은 상태를 관리해야 함(DOM)
- 웹 개발시 DOM, 상태값 관리를 최소화하고 기능구현에만 집중하게 함

프레임워크 : 개발구조나 설계 시 제공되는 인터페이스의 집합
라이브러리 : 특정 기능에 대해 API(도구/함수)를 모은 것

```javascript
import React from "react";
import "./styles.css";

function App() {
  const user = {
    firstName: "React",
    lastName: "JSX Activity"
  };

  function formatName(user) {
    return user.firstName + " " + user.lastName;
  }
  // JSX 없이 활용한 React
  return React.createElement("h1", null, `Hello, ${formatName(user)}!`);
  // HTML과 JS로 나누어 있어 복잡함

  // JSX 를 활용한 React
  return <h1>Hello, {formatName(user)}!</h1>;
  // JSX에서 한번에 처리할 수 있어 
  // 코드의 복잡성을 줄이고, 이해하기 쉽게 만들 수 있음

}

export default App;
```

### 태그는 반드시 닫혀 있어야 함

- html에서 클로징이 없는 input, br태그도 닫아줘야함
- <input /> 같은 형태로 셀프 클로징 태그도 가능

### 감싸져 있는 엘리먼트

- 두 개 이상의 엘리먼트는 무조건 하나의 엘리먼트로 감싸져 있어야 함
- <div> 태그 사용 어려울 시 <Fragment>로 감쌀 수 있음 (단, 상단에서 import 한 후에 사용가능)

### 자바스크립트 값 사용시에는 중괄호 사용

- name 변수의 값을 사용하려면 {name} 형태로 표기
- 중괄호 내에서 if문 사용을 위해 삼항연산자 사용

```javascript
{
  x === 1 ? <div>x는 1입니다</div> : <div>x는 1이 아닙니다</div>;
}
// {판별 조건 ? (참일 때 출력값) : (거짓일 때 출력값)}
```

- true일 때만 보여주려면 AND연산자 사용

```javascript
{
  x === 1 && <div>x는 1입니다</div>;
}
// {판별조건 && 참일 때 출력 값}
```

- 꼭 필요한 경우에는 즉시 실행 함수 표현(IIFE) 사용  
  (복잡한 조건의 경우 되도록 JSX 밖에서 로직 작성)

```javascript
<div>
  {(function () {
    if (x === 1) return <div>하나</div>;
    if (x === 2) return <div>둘이다</div>;
    if (x === 3) return <div>셋이다</div>;
  })()}
  // {(function(){함수의 내용})()}
  // 동일하게 중괄호로 감싸고 익명함수 즉시 실행('()')
</div>
```

- 화살표 함수 사용 시 좀더 간략시 표현 가능

```javascript
<div>
  {() => {
    if (x === 1) return <div>하나</div>;
    if (x === 2) return <div>둘이다</div>;
    if (x === 3) return <div>셋이다</div>;
  }()}
  // {(() => {함수의 내용})()}
  // 화살표함수는 this, argument, super 개념이 없는 익명함수
</div>
```

- 스타일 설정은 항목은 카멜케이스 값은 ''안에 텍스트로 작성

```javascript
class App extends Component {
  render() {
    const style = {
      backgroundColor: "black",
      padding: "16px",
      color: "white",
      fontSize: "36px",
    };
    return <div style={style}>안녕하세요!</div>;
  }
}

export default App;
```

- 주석은 멀티라인을 중괄호로 감싸거나 태그사이에 // 넣기

```javascript
class App extends Component {
  render() {
    return <div className="App">리액트</div>;
  }
}
```

- 클래스명은 <className = "">형태로 작성

```JSX
class App extends Component {
  render() {
    return (
      <div>
      {*/ 멀티라인 방식의 주석 */}
      <h1 //태그 사이 방식의 주석 >리액트</h1>
      </div>
    )
  }
}
```

### (React) JSX 문법을 잘못 사용하고 있는 예제를 고르세요

```javascript

JSX 문법을 잘못 사용하고 있는 예제를 고르세요

A.
const Hello = () => {
    return (
        <div>안녕하세요</div>
    )
}

B.
const Hello = () => {
    return (
        <div>안녕하세요</div>
        <div>반갑습니다</div>
    )
}


C.
const Hello = () => {
    const name = 'walli'
    return (
         <div>안녕하세요 {name} 입니다.</div>
    )
}

D.
const Hello = () => {
    return (
        [<div>안녕하세요</div>,<div>반갑습니다.</div>]
    )
}


정답 (B)

A : 하나의 JSX 표현식 -> 감싸는 태그 필요 X
B : 두 개 이상 엘리먼트 -> 감싸는 태그
C : 변수를 {} 안에 넣어줘서 옳은 문법
D : 배열의 각 요소는 각각 변수에 담길 수 있는 JSX 표현식

```

### 아래 화면을 출력하기 위한 코드 중 틀린 것은?

<img src="https://s3.ap-northeast-2.amazonaws.com/urclass-images/pCeQIG0Nx-1617339990014.png" width="100px" height="100px">

```javascript

JSX 문법을 잘못 사용하고 있는 예제를 고르세요


A.
let langs = ["JavaScript", "HTML", "Python"];
  let viewLangs = () =>  {
    return langs.map((it) => {
      return <p>{it}</p>;
    });
  };

  return (
    <div>
      {viewLangs}
    </div>
  );

B.
let langs = ["JavaScript", "HTML", "Python"];

  let viewLangs = langs.map((it) => {
      return <p>{it}</p>;
    });

  return (
    <div>
      {viewLangs}
    </div>
  );

C.
let langs = ["JavaScript", "HTML", "Python"];

  return (
    <div>
       {langs.map((it) => {
        return <p>{it}</p>;
      })}
    </div>
  );

D.
let langs = ["JavaScript", "HTML", "Python"];
  return (
    <div>
      {langs.map((it) => (
        <p>{it}</p>
      ))}
    </div>
  );


정답 (A)

A :  viewLangs 가 화살표 함수 표현식으로 선언 -> 함수를 호출하는 연산자 () 를 써야 작동
B : map 함수 호출 결과를 viewLangs 변수에 잘 담음
C : 변수를 {} 안에 넣어줘서 옳은 문법 
중괄호를 사용하여 JavaScript를 내부에 표현해주었기 때문에 올바르게 작동합니다. 주의할 점은 중괄호를 쓰게 되면 JavaScript 코드로 인지하므로 C의 경우 꼭 return 이 존재해야 합니다. return 이 없다면 undefiend 를 반환하게 됩니다. 정리하자면 중괄호({}) 를 묶으면 function () {}와 같으며, 소괄호(())로 묶으면 () 안의 값이 return값이 됩니다.
D : C와 마찬가지로, () 를 사용했기 때문에 () 안의 값이 return 값이 됩니다.

```