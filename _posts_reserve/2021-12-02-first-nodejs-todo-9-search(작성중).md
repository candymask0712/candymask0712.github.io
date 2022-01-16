---
title: "[Nodejs lecture 1] todo app 만들기 - 9 (검색)"
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

## **회원가입 기능 추가하기(세션방식)**

    - 회원가입 기능 구현을 위한 미들웨어 설치
    -

### 1. 미들웨어 설치 및 사용

    - `npm install passport passport-local express-session`로 설치
    - 서버파일에 미들웨어 사용

    - 기존 list페이지에 검색창 추가 및 검색 버튼 누를 시 액션 추가

sdfasdfasdfasdfasdfa

    ```JavaScript
    // list.js
    <div class="container input-group mb-2">
      <input class="form-control">
      <button class="input-group-append btn btn-danger" id="search">검색</button>
    </div>
    <script>
      $('#search').click(function(){
        // 아이디가 search인 버튼을 클릭 시 아래 내용 실행
        var 입력한값 = $('search-input').val()
        //  input의 입력값을 가져오는 코드
        window.location.replace('/search?value=' + 입력한값)
        // '/search'가 실행 됨(해당 url은 get요청으로 셋팅)
      })
    </script>
    ```

### 2. 로그인페이지 제작 및 & 라우팅

    - `npm install method-override` 명령어로 설치

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
