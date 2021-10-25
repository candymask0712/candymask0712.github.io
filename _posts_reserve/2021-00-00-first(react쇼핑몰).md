---
title: "[] "
excerpt: "21년 00월 00일 공부일지 (소제목)"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - 
tags:
  - 
  -
last_modified_at:
---

### **1.**
1. 프로젝트 설명
   npx create-react-app 폴더명
   yarn create-react-app 폴더명 (더 빠름)

### **2. import/export 사용법**
- 파일 간 변수/데이터 이동 시 사용

1. 내보내기 : export default 변수명
- 변수명, 함수명, 자료형 모두 export 가능
- 파일마다 export default 키워드는 한번만 사용 가능
  
    ```javascript
    var Data = 'A';
    export default Data;    
    ```
2. 가져오기 : import {변수명} from 경로
   - export default로 내보낸 경우 {} 생략가능
   
    ```javascript
    var Data = 'A';
    export default Data;
    ```    

여러 개를 내보내는 경우 
- 내보내기 export {변수1, 변수2}
- 가져오기 import {변수1, 변수2} from 경로
- 어려 개의 변수를 내보낼 때는 그냥 자료형이 아닌 변수명이 반드시 있어야 함

### **3. Component 제작**
1. function 컴포넌트명() {}
2. return (<div></div>)
3. 필요한 곳에 <컴포넌트명 />

### **3. props로 state 전송법**
1. <자식컴포넌트 보낼이름={전송할state} />
2. function 자식컴포넌트(props){}
3. props.보낼이름
  ```javascript
  function Parent (){
    const obj = {name: 'a', age: 1}
    const [list, setList] = useState(obj);
    <Children sendName={list}/>
  }
  const Children = props => {

    return (
      <div> 
      {props.sendName.name} 
      {props.sendName.age}
      </div> 
    )
  }
  ```

  - 비구조화 할당 시
  ```javascript
  const Children = props => {
  const { name, age } = props.sendName
    return (
    <div> 
      {name} 
      {age}
    </div> 
    )
  }
  ```
- 예시 작성
- i 활용 방법


### **4. react router**
1. 기본셋팅
  - 설치 : yarn add react-router-dom
  - import하기
  ```javascript
  (...) // index.js 파일 내에서  
  import { BrowserRouter } from 'react-router-dom';
  // from 뒤에 경로 없음 : 라이브러리임
  ```
  - 컴포넌트 추가
  ```javascript
  (...) // index.js 파일 내에서
    <BrowserRouter>
     <App />
    </BrowserRouter>
  ```
  Hash router : 라우팅을 안전하게 해줌
  - 주소창은 서버에 데이터를 요청하는 공간
  - 주소창에 #이 추가됨(# 뒤 내용은 서버에 전송 x)
  
2. Route 만들기(페이지 나누기)
  - 필요한 것들 import 하기
  ```javascript
  (...) // app.js 파일 내에서
  import { Link, Route, Switch } from 'react-router-dom'
  ```
  - Route에 경로 연결하기
  ```javascript
    <Route path="경로">HTML 작성</Route>
  ```
  - exact 속성 추가시 정확히 일치하는 경로로 적용
  ```javascript
    <Route exact path="경로">HTML 작성</Route>
  ```

3. Link 연결하기
  - 기본 설정
  ```javascript
  (...) // app.js 파일 내에서
  <Link to="경로">버튼/글자</Link>
  ```
  ```javascript
  (...) // index.js 파일 내에서
  import { Link, Route, Switch } from 'react-router-dom'
  ```
  - 다른 방법으로 이동시키기
  ```javascript
  (...) // index.js 파일 내에서
  import { useHistory } from 'react-router-dom';
  (...)
  let history = useHistory();
  (...)
  <button className="btn btn-danger" onClick={() => {
    history.goBack();
  }}>뒤로가기</button> 
  // goback 부분 바꾸면 다양한 동작 가능
  // push('경로') 하면 특정 경로로 이동가능
  ```

  - Switch로 연결
    - 해당되는 Link가 여러 개라도 맨 위 것만 보임
    - 보통 Link 들을 <switch>로 감싸서 사용

4. URL 파라미터 사용하기
  
  ```javascript
  /detail/:id
  // 아무문자나 받겠다는 URL 작명법
  // 1. 콜론 뒤에 맘대로 작명
  // 2. 여러개 사용 가능
  // detail/:id1/:id2
  ```

### **5. styled-components**
1. styled-components 
- class 선언 없이 컴포넌트에 CSS를 직접 장착
- CSS in JS라고도 부름
- 장점 : className 작명 필요x, css요소 간 간섭 없음
- 단점 : 엘리먼트마다 컴포넌트로 변환 필요
  1. 기본셋팅
    - yarn add styled-componenets 로 설치
    - import styled form 'styled-components' 로 가져옴
  2. 사용법
    - 상단 위치에 선언하기(백틱 사용)
    ```javascript
    let 박스 = styled.div`
        padding: 20px;
      `;
      //'박스'라는 이름의 <div>태그를 생성
      // padding은 20px로 설정
    ```
    - 원하는 위치에 컴포넌트 사용
    ```javascript
      return (
      <div>
        <div className="container">
          <박스>예시</박스>
        <div>
    ```
  3. 활용
    - 특성 하나만 바꿔 재활용 (템플릿리터럴 활용)
    ```javascript
      let 제목 = styled.h4`
        color: ${props => props.색상};
      `;
    ```
    - 원하는 컴포넌트에서 props 보내주기
      ```javascript
          return (
            <div>
                <박스>
                  <제목 색상="blue">Detail</제목>
                  <제목 색상="red">Detail</제목>
                </박스>
            <div>
        ```

  
    - import styled form 'styled-components' 로 가져옴  

### **6. SASS**
  - CSS를 프로그래밍 언어처럼 다룰 수 있는 대체문법
  - 브라우저가 읽을 수 있게 CSS로 컴파일 필요
  
  1. 준비과정
    - 컴파일을 위한 node-sass 설치 
      ```javascript
      yarn add node-sass
      ```
    - sass 파일 생성 후 import
      ```javascript
      import './Detail.scss';
      ```
  2. 활용
    - 색상 등 반복변수는 저장해 활용
      ```scss
        $변수명 : 변수에 넣을 값
        $maincolor : #ff0000;

        .red {color: $maincolor}
      ```

    - @import를 이용한 파일경로 설정
      ```scss
        @import './_reset.scss';
        // reset 등 자주 사용표현들 저장해 사용
        // 이런파일은 _를 앞에 표시
      ```

    - nesting 문법
      : 셀렉터 해석이 쉽고  
        관련 된 class 끼리 관리 쉬움
      ```scss
      // 일반 css 선택자
      div.container h4 {
          color : blue;
        }
      div.container p {
        color : green;
      }
      ```
      ```scss
      // nesting 문법 적용 시
      div.container {
        h4 {
          color : blue;
        }
        p {
          color : green;
        }
      }
      ```
    - @extend 문법
      : 반복되는 특성 손쉽게 관리
      ```scss
      .my-alert {
        background : #eeeeee;
        padding : 15px;
        border-radius : 5px;
        max-width : 500px;
        width : 100%;
        margin : auto;
      }
      .my-alert2 {
        @extend .my-alert;
        background : yellow;
      }
      // my-alert의 속성이 그대로 전달
      ```
    - @mixin 문법
      : 함수 형태로 반복되는 특성 손쉽게 관리
      ```scss
      @mixin 함수() {
        background : #eeeeee;
        padding : 15px;
        border-radius : 5px;
        max-width : 500px;
        width : 100%;
        margin : auto;
      }
      .my-alert {
        @include 함수()
      }
      // 함수의 특성이 my alert로 그대로 전달
      ```

[참고자료 - SASS문법(extends & mixin)](http://megaton111.cafe24.com/2017/01/13/sass-%EB%AC%B8%EB%B2%95-%EB%B6%88%EB%9F%AC%EC%98%A4%EA%B8%B0import-%EC%83%81%EC%86%8Dextend-%EB%AF%B9%EC%8A%A4%EC%9D%B8mixin/)
### **7. useEffect의 활용**
1. useEffect의 사용
  - 컴포넌트가 mount/update 시 특정 코드 실행  
  - setTimeout과 함께 사용 시 다양하게 활용 가능  
    ex) 특정 페이지 방문 후 n초 내에 사라지는 알람 등  
    ```javascript
      setTimeout(()=>{실행할코드},시간(ms단위))
    ```


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