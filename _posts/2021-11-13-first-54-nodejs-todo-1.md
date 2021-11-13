---
title: "[Nodejs] todo 앱 만들기 -1"
excerpt: "21년 월 일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs
tags:
  - Nodejs
  - JS
  - TIL
last_modified_at:
---

## **1. 프로젝트 시작**

### 1. 디렉토리 생성 및 설치

- npm init 으로 시작 (server이름만 원하는 이름으로 설정 server.js)

- server.js 파일 생성(최상위 디렉토리)

```javascript
const express = require('express');
const app = express();
// 서버를 만들기 위한 기본문법

```

### 2. 기본 서버요청 구현

- listen으로 기본 포트번호 구현
- get사용하여 페이지별 보여줄 내용 구성

```javascript
app.listen(8080, function{
// listen(서버띄울 포트번호, 띄운후 실행할 코드)
})

app.get('/pet', function(요청, 응답){
  응답.send('사이트입니다')
})
// http://localhost:8080/pet 접속 시
// '사이트입니다' 라는 메세지가 나옴

// 요청들은 node 파일명.js 로 실행 후 반영 됨
```

## **2. 기본 준비**

### 1. nodemon으로 서버 재실행 자동화

```bash
npm install -g nodemon
// -g는 전역설치 시 사용하는 명령어
```

```bash
nodemon server.js
// 해당 파일 내 포트 자동업데이트

```

### 2. url별 html 파일 연결하기

```javascript
app.get('/', function(요청, 응답){
  응답.sendFile(__dirname + '/index.html')
})
// http://localhost:8080/ 접속 시 index.html 파일 내용이 보임
```

### 3. bootstrap으로 기본 스타일링

- 아래 url에서 Starter template을 html에 복사   
[bootstrap 홈페이지](https://getbootstrap.com/docs/5.1/getting-started/introduction/)

### 4. post 요청하기

`app.post('경로',콜백함수)` 형태로 사용
```javascript
<form method="POST" class="form-inline my-2 my-lg-0" />
// 액션일어나기 원하는 태그에 method와 class 꼭 지정해주기
// /add 경로로 post를 요청하게 됨

// ser
app.post('/add', function(요청, 응답){
  응답.send('전송완료')
})
// input에 적은 정보는 '요청' 부분에 저장 됨
```
### 5. body-parser를 이용한 내용 전달                          
                                         

$ npm install body-parser 설치

```javascript
const bodyParser = require('body-parser');
app.use(express.urlencoded({extended: true})) 

// 사용을 위해 서버파일 최상단에 기재
```

- name속성으로 input에 이름 쓰기
```javascript
// html 파일
<div class="form-group">
  <label>오늘의 할일</label>
  <input type="text" class="form-control" name="title">
</div>
<div class="form-group">
  <label>날짜</label>
  <input type="text" class="form-control" name="date">
</div>
// 사용을 위해 서버파일 최상단에 기재
```

```javascript
app.post('/add', function(요청, 응답){
  응답.send('전송완료')
  console.log(요청.body.title)
})
// 요청.body.정한이름 으로 데이터 들어옴
```
