---
title: "[Nodejs lecture 1] todo app 만들기 - 2 (MongoDB통한 서버통신)"
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

## **1. MongoDB 연결 및 기본사용**

### 1. 디렉토리 생성 및 설치

- MongoDB 사이트 접속하여 기본 설정
  https://www.mongodb.com/

- 아래 명령어를 통해 MongoDB 설치

  ```shell
  npm install mongodb
  ```

- 아래 코드를 통해 server파일에 MongoDB 연동

  ```javascript
  const MongoClient = require("mongodb").MongoClient;
  // 상단에 몽고 디비 연동을 위해 작성

  MongoClient.connect(
    "몽고디비에서 제공하는 코드 작성",
    function (에러, client) {
      "몽고디비 연결 시 작동해야 하는 코드";
    }
  );
  // 몽고디비의 실제 사용 방법
  ```

### 2. database에 자료 저장하기

- MongoDB 사이트 collection 메뉴에서 기본설정
- database는 폴더, collection은 파일과 비슷한 역할

  ```javascript
  let 변수명;
  // connect 밖에 변수 생성

  MongoClient.connect(
    "몽고디비에서 제공하는 코드 작성",
    function (에러, client) {
      변수명 = client.db("todoapp");
      // 'todoapp'이라는 database에 연결요청
      변수명.collection("post").insertOne("데이터", function (에러, 결과) {
        console.log("저장완료");
      });
      // collection이라는 database에 '데이터'부분을 저장
      // 이 때 '데이터'는 반드시 객체 형식이여야 함
      // 객체 전달 시 키를 '_id'로하면 MongoDB에 반영 됨
      // 미 기재시 랜덤한 id가 배정 됨
    }
  );
  ```
