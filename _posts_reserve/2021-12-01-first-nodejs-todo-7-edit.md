---
title: "[Nodejs lecture 1] todo app 만들기 - 7 (글 수정 기능 추가)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs lecture 1
tags:
  - Nodejs
  - JavaScript
last_modified_at:
---

## **글 수정 기능 추가하기**

    - 수정에 해당하는 ejs 파일 만듬
    - /:id 방식으로 글 번호에 해당하는 페이지로 이동 시킴

### 1. 수정 기능 용 ejs 파일 만들기

    - 제목 및 날짜 수정을 위해 기존 write와 유사하게 작성
    - 여기에 edit을 위한 요청부분과 id부분 추가

    ```JavaScript
    // edit.ejs
    <div class="container mt-3">
      <form action="/edit?_method=PUT" method="POST">

        <div class="form-group">
          <label>id</label>
          <input type="number" class="form-control" name="id" value="<%= data._id %>" style="display: none;">
    ```

### 2. list 페이지에서 상세페이지 이동 기능 만들기

    ```JavaScript
    // list.ejs
    <h4 class="ml-2 my-3">서버에서 가져온 할 일 리스트</h4>
    <ul class="list-group">
      <% for(let i = 0; i < posts.length; i++ ){ %>
      <a href="http://localhost:8080/detail/<%= posts[i]._id %>">
        <li class="list-group-item">
          <p>글번호 : <%= posts[i]._id %></p>
          <h4>할 일 제목 : <%= posts[i].제목 %></h4>
          <p>할 일 마감날짜 : <%= posts[i].날짜 %></p>
          <button class="delete" data-id="<%= posts[i]._id %>">샥제</button>
        </li>
      </a>
      <% } %>
    </ul>
    ```

### 3. detail페이지 이동시 서버에서 보내 줄 데이터 처리

    ```JavaScript
    // server.js
    app.get('/detail/:id', function(요청, 응답){
      // /뒤에 ':'을 입력하면 /뒤에 아무 내용이나 입력해도 이동하라는 명령
      // ':' 뒤에 붙은 id는 원하는 대로 작명 가능
      요청.params.id = Number(요청.params.id)
      // 몽고디비에 있는 id와 요청의 id의 타입이 다름
      // 항상 타입처리에 대해 신경써야함
      // vs code에서 보내는 값에 커서를 올리면 대략적으로 확인 가능
        db.collection('post').findOne({_id: 요청.params.id}, function(에러, 결과){
          if(에러){
            응답.render('detail.ejs', {에러: 에러})
          console.log(결과)
          } else {
            응답.render('detail.ejs', { data : 결과 })
          }
        })
        // 요청이 들어오면 {}안에있는 데이터를 보내고 ejs파일을 렌더링
    });
    ```

[참고자료 - codingapple Nodejs 강의](https://codingapple.com/course/node-express-mongodb-server/)
