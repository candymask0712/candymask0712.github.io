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

5. useEffect의 사용
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