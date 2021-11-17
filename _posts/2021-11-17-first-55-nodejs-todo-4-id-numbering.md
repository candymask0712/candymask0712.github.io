---
title: "[Nodejs lecture 1] todo app 만들기 - 4 (id 번호달기)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs lecture 1
tags:
  - id numbering
  - Nodejs
  - JavaScript
last_modified_at:
---

## **1. DB데이터 읽기**

### 1. 전체 데이터 읽기

```javascript
app.get("/list", function (요청, 응답) {
  db.collection("post")
    .find()
    .toArray(function (에러, 결과) {
      console.log(결과);
    });

  응답.render("list.ejs");
});
```

- DB데이터 출력시 사용하는 코드의 의미

```javascript
  db.collection('post').find().toArray(function(에러, 결과){
    console.log(결과);
  })

  db.collection('post')
  // DB에 있는 post라는 collection과 연계 시 필수 작성

  .find()
  //find()는 모든 데이터를 가져올 때 사용

  .toArray()
  // 서버에 있는 메타데이터 등을 제외하기 위한 코드

  function(에러, 결과){}
  // 콜백함수에는 두 개의 파라미터가 들어감
  // 첫 번째 파라미터 - 에러가 났을 때 에러를 출력하는 용도
  // 문제 발생 시 에러 부분을 콘솔에 출력하면 됨
  // 두 번째 파라미터 - 실제 결과를 담고 있는 부분
```

```javascript
// server.js
app.get("/list", function (요청, 응답) {
  db.collection("post")
    .find()
    .toArray(function (에러, 결과) {
      응답.render("list.ejs", { posts: 결과 });
      // list.ejs 파일로 post라는 키의 결과라는 value를 담아 전달
      // render 메서드를 이용해 ejs파일로 결과를 전달
      // 결과부분은 보통 객체 형태로 전달함
    });
  // render 메서드 부분은 반드시 db.collection안에 들어 있어야 함
  // 전송하고 있는 '결과'라는 변수가 함수 클로저 안에 있음
});
```

```javascript
// list.ejs
<% for(let i = 0; i < posts.length; i++ ){ %>
  <h4>할 일 제목 : <%= posts[i].title %></h4>
  <p>할 일 마감날짜 : <%= posts[i].date %></p>
<% } %>
// 반복문을 사용하여 ejs 파일에서 데이터를 표기
// 값을 표기할 때는<%= 원하는 값 %>>
// 구문을 표기할 때는 '='를 빼고 <% 원하는 구문 %>>
```

[참고자료 - codingapple Nodejs 강의](https://codingapple.com/course/node-express-mongodb-server/)
