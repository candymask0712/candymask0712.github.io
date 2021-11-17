---
title: "[Nodejs lecture 1] todo app 만들기 - 3 (EJS)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs lecture 1
tags:
  - Nodejs
  - JavaScript
  - ejs
last_modified_at:
---

## **1. EJS 기본셋팅**

### 1. EJS 설치

- 아래 명령어를 통해 디렉토리에 EJS 설치

  ```shell
  npm install ejs
  ```

- 아래 코드를 통해 server파일에 EJS 연동

  ```javascript
  app.set("view engine", "ejs");
  ```

- 기존 html 파일의 확장자를 .ejs로 변경
  - .ejs 확장자는 html 기능 쓰면서도 서버데이터 삽입 가능

### 2. EJS 사용

- 기존 html 파일의 확장자를 .ejs로 변경

  - .ejs 확장자는 html 기능 쓰면서도 서버데이터 삽입 가능

- .ejs 파일은 반드시 views 폴더를 생성해서 그 안에 삽입

- `%`기호를 이용해 데이터 삽입
  `<%= 서버에서 보낸 데이터의 변수명 %>`

  ```html
  // list.ejs
  <h2><%= user.name %></h2>
  ```

- 서버파일 상단에 ejs 사용을 위한 코드 작성

  ```javascript
  // server.js
  app.set("view engine", "ejs");
  ```
