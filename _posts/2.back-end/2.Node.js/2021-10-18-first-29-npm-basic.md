---
title: "[Node.js] Node.js 기초 - 패키지 개념과 npm"
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs
tags:
  - nvm
  - npm
last_modified_at:
---

### **1. 런타임과 Node.js**
- 런타임 : 프로그래밍 언어가 구동되는 환경 (웹 브라우저 등)
- Node.js : JS런타임 (웹 브라우저가 아닌 환경에서 JS 실행시켜 줌)

### **2. nvm과 npm**
  1. nvm  
- Node Version Manager의 약자로 노드의 버젼관리 프로그램
- 노드 버전에 따라 생기는 에러 상황에서 쉽게 버젼관리 가능

  2. npm  
- Node Package Manager의 약자로 노드의 기본 패키지 관리자 역할
- node.js에 필요한 모듈를 다운 할 수 있는 일종의 모듈스토어
- package.json에는 실행에 필요한 모듈, 실행 방법, 테스트 방법이 명시됨 (실제 모듈은 node_modules 폴더에 저장) ->**협업에 필수적**
- npm install 명령어로 package.json에 명시된 모듈 다운 가능

- package.json의 주요내용
  1) devDependencies : 개발하는 환경에서 필요한 모듈
   (npm install로 모듈 설치 시  --save-dev 옵션과 쓰면 devDependencies 에 리스트 추가 됨)
  2) dependencies : 프로젝트 구동 시 필수 모듈
    (~~--save 옵션과 설치 시 dependencies에 리스트 추가 됨~~, 현재는 자동으로 추가됨)
  3) scripts : CLI에서 사용가능한 명령 기술  
     
      |작업내용|제목 셀2|
      |---|---|
      |node.js 앱 실행|npm run start|
      |테스트 실행|npm run test|
      |코드검사|npm run lint|
      |과제제출*|npm run submit|
      * 과제제출은 부캠 한정

### **3. node.js 사용**
- (터미널 환경에서) node 파일명.js로 실행가능