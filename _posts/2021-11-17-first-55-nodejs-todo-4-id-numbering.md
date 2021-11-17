---
title: "[Nodejs lecture 1] todo app 만들기 - 4 (ID 번호달기)"
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

## **1. ID 번호달기**

### 1. MongoDB에 collection생성

- MongoDB에 id관리를 위한 별도 collection생성

```javascript
// MongoDB collection
{_id : 619301e7254a0147844261c7,
totalPost : 0,
name : "게시물 갯수" }
```

- sever파일에서 해당 collection 연동

```javascript
  db.collection('counter').findOne({name : "게시물 갯수"})
  // counter collection에서 "name"이라는 프로퍼티 하나만 찾기
```

- 게시글 업로드마다 id이 값이 1씩 더해지도록 연동

```javascript
db.collection('counter').updateOne({수정할데이터},{수정할 값},function(){})
// mongoDB에 있는 값을 수정할 때 사용하는 unpdate함수의 사용법
// 한 개만 수정할 때는 updateOne, 여러 개 수정 시는 updateMany 사용
// 총 세 개의 인자를 넣을 수 있고 마지막 콜백 함수는 옵션

db.collection('counter').updateOne({name:'게시물 갯수'},{ $inc : {totalPost:1}},function(에러, 결과){
  
})
// 수정할 값에 operator 이용하여 값 변경
// 문법에 따라 값은 다시 중괄호로 감싸야 함

// mongoDB의 operator 종류
// $set (변경)
// $inc (증가)
// $min (기존 값보다 적을 때만 변경)
// $rename (key 값 이름 변경)
```



[참고자료 - codingapple Nodejs 강의](https://codingapple.com/course/node-express-mongodb-server/)
