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

### **1. MongoDB 연결하기**

1. 디렉토리 생성 및 설치

- MongoDB 사이트 접속하여 기본 설정
  https://www.mongodb.com/

- 

- 아래 명령어를 통해 server파일에 MongoDB 연동

```javascript
const MongoClient = require('mongodb').MongoClient;
// 상단에 몽고 디비 연동을 위해 작성

MongoClient.connect('몽고디비에서 제공하는 코드 작성', function(에러, client){
'몽고디비 연결 시 작동해야 하는 코드'
})
// 몽고디비의 실제 사용 방법

```
