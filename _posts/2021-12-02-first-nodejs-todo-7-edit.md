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
    <form action="/edit?_method=PUT" method="POST">
    // HTML에서는 get, post 요청만 가능
    // 그 외 요청을 위해서 method-override 사용
    <div class="form-group">
      <label>id</label>
      <input type="number" class="form-control" name="id" value="<%= data._id %>" style="display: none;">
    // edit 시 글을 특정하기 위해 id 값 추가(보이지 않게 처리)
    </div>
    ```

### 2. method-override 설치 및 사용

    - `npm install method-override` 명령어 이용 설치

    ```JavaScript
    // server.ejs
    const methodOverride = require('method-override')
    app.use(methodOverride('_method'))
    // 서버 파일 상단에 미들웨어 사용 명시
    ```

### 3. edit 처리를 위한 서버쪽 코드 작성

    ```JavaScript
    // server.js
    app.get('/edit/:id', function(요청, 응답){
     // edit 뒤에 어떤 문자가 오더라도 edit.ejs를 렌더링해 보여줌
      요청.params.id = Number(요청.params.id)
      // 요청은 url에서 파라미터의 형태로 들어옴
      // 파라미터로 들어온 id값을 숫자로 변환
      // 인자 전달 시에는 항상 타입체크 중요
        db.collection('post').findOne({_id: 요청.params.id}, function(에러, 결과){
        // post 콜렉션에서 id가 요청.params.id과 일치하는 데이터 찾기
            응답.render('edit.ejs', { data : 결과 })
            // DB에 요청한 값은 결과라는 이름으로 들어옴
            // 찾은 데이터를 객체에 담아 data라는 이름으로 전달
        })
    });

    app.put('/edit', function(요청, 응답){
      let num = Number(요청.body.id)
      db.collection('post').updateOne({_id: num}, { $set : {제목 : 요청.body.title, 날짜 : 요청.body.date}},
      // post 컬렉션에서 수정된 제목과 날짜로 값을 바꿈
      function(에러, 결과){
        db.collection('post').findOne({_id: num}, function(에러, 결과){
          응답.redirect('/list')
          // 수정을 한 뒤 빈 페이지 대신 list로 연결
        })
      });
    })
    ```

[참고자료 - codingapple Nodejs 강의](https://codingapple.com/course/node-express-mongodb-server/)
