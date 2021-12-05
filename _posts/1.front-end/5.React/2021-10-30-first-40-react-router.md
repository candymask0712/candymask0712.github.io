---
title: "[React] SPA & Route"
excerpt: "21년 10월 30일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - router
  - switch
last_modified_at:
---

### **1.SPA란**

- 서버로부터 페이지 갱신에 필요한 데이터만 받아 업데이트하는 웹사이트 또는 웹 어플리케이션
- Single Page Application 의 약자
- 사용자의 인터렉션에 빠르게 반응 + 서버부담 적어짐
- JS파일 무거워짐(느린 첫화면 로딩) / SEO에 불리함

### **2. React Router**

- 라우팅 : 다른 주소에 따라 다른 뷰를 보여주는 과정
- React에서는 React Router라는 라이브러리 사용  
 `npm install react-router-dom` 

|컴포넌트 명|역할|
---|---
|BrowserRouter|Hisroty API이용 route사용하게 해줌|
|Switch|경로 일치하는 단 하나의 라우터만 렌더링|
|Route|path에 어떤 컴포넌트 보여줄지 결정|
|Link|새로고침 없이 경로를 연결 해줌|
  
1. route의 exact 속성
React router의 특성상 exact속성이 없으면 해당 경로(예시의 "/")로 시작하는 중복된 `<Route>` 컴포넌트를 모두 보여줍니다. exact는 주어진 경로와 정확히 일치해야만 설정한 `<Route>` 컴포넌트를 보여주는 역할

1. switch의 역할

`<Switch>` 를 사용하여 exact 역할을 대신 해줄 수 있음. 하지만 `<Switch>`는 순서와 위치가 중요합니다(위에서 아래로 경로를 하나씩 검사하면서 해당 경로에 해당하는 라우트를 실행)
만약 위의 예제처럼 Home을 위에 둔 상태에서 exact없이 활용한다면 중복되는 경로로 인해 다른 라우트로의 이동이 불가능한 것을 확인하실 수 있음

```javascript
function App () {
  return (
   <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              Home
            </li>
            <li>
              MyPage
            </li>
            <li>
              Dashboard
            </li>
          </ul>
        </nav>
      <Switch>
          <Route exact path="/">
            <Home />
          </Route>
          <Route path="/about"> {/* 경로를 설정 */}
            <MyPage /> {/* 컴포넌트 연결 */}
          </Route>
          <Route path="/dashboard">
            <Dashboard />
          </Route>
        </Switch>
      </div>
   </BrowserRouter>
  )
}

export default App;
```
