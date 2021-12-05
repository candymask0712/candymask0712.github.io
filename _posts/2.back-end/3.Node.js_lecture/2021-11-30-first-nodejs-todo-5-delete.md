---
title: "[Nodejs lecture 1] todo app 만들기 - 5 (글 삭제하기)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs lecture 1
tags:
  - delete
  - Nodejs
  - JavaScript
last_modified_at:
---

## **1. 글 삭제하기**

    - HTML에서는 GET/POST요청만 가능
    - DElETE를 위해서는 method-override 라이브러리 또는 AJAX 요청 필요

### 1. 리스트에 삭제버튼 추가 및 스타일링

    ```JavaScript
    // list.ejs
    <h4 class="ml-2 my-3">서버에서 가져온 할 일 리스트</h4>
    // 부트스트랩 사용시 간단하게 CSS 스타일링도 가능
    // ml로 margin left, my로 margin-y 설정

    <ul class="list-group">
      <% for(let i = 0; i < posts.length; i++ ){ %>
      <li class="list-group-item">
        <h4>할 일 제목 : <%= posts[i].제목 %></h4>
        <p>할 일 마감날짜 : <%= posts[i].날짜 %></p>
        <button>샥제</button>
      </li>
      <% } %>
    </ul>
    // 버튼 생성 및 부트스트랩 스타일링 적용
    ```

### 2. jQuery를 사용한 DELETE 요청

    - jquery 사용을 위해 스크립트 작성

    ```javascript
    // list.ejs
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.min.js"></script>
    ```

    - jquery의 ajax을 사용하여 요청 부분 작성

    ```javascript
    // list.ejs
    <script>
      $.ajax({
        method : 'DELETE',
        url : '/delete',
        data : {_id : 1}
      }).done(function(결과){

      })
    </script>
    ```
    - 서버파일에서 요청에 따른 삭제 기능 구현

    ```JavaScript
    // server.js
    app.delete('/delete', function(요청, 응답){
      db.collection('post').deleteOne( 삭제할 내용 , function(에러, 결과){
          console.log('삭제완료')
        // 삭제시 같이 실핼할 내용
      })
    })
    ```

    - 서버파일에서 요청에 따른 삭제 기능 구현

    ```JavaScript
    // server.js
    app.delete('/delete', function(요청, 응답){
      db.collection('post').deleteOne( 삭제할 내용 , function(에러, 결과){
          console.log('삭제완료')
        // 삭제시 같이 실핼할 내용
      })
    })
    ```

    - 서버파일에서 요청에 따른 삭제 기능 구현

    ```JavaScript
    // server.js
    app.delete('/delete', function(요청, 응답){
      요청.body._id = parseInt(요청.body._id)
      // { _id : '1' } 같이 AJAX 요청에서 id가 문자화 됨
      // parseInt를 사용해 문자를 숫자화해야함
      db.collection('post').deleteOne(요청.body, function(에러, 결과){
        // { _id : '1' } 인 자료 삭제(요청.body에 들어있음)
          console.log('삭제완료')
      })
    })
    ```

    - AJAX요청임에도 사용자가 즉각 삭제반영여부 볼 수 있게 처리
    - 실패 시 에러 메세지 출력되도록 처리

    ```JavaScript
    // list.ejs
      $('.delete').click(function(e){
        let 글번호 = e.target.dataset.id;
        let 지금누른거 = $(this)

        $.ajax({
          method : 'DELETE',
          url : '/delete',
          data : {_id : 글번호}
          }).done(function(결과){
            console.log('성공했어요')
            지금누른거.parent('li').fadeOut();
          }).fail(function(a,b,c){
            console.log(a,b,c)
            console.log('실패했어요')
        })
      })
    ```

[참고자료 - codingapple Nodejs 강의](https://codingapple.com/course/node-express-mongodb-server/)
