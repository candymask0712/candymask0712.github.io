---
title: "[Nodejs] Nodejs에서 디버깅하기"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Nodejs
tags:
  - debugger
last_modified_at:
---

### **1. 웹으로 node.js 디버깅하기**

- console.log로 객체 조회 시 모든 매서드가 나와 불편
- 아래 명령어를 통해 디버깅 시작

```javascript
node --inspect 파일명
// 실행 시 debugging listening on '주소' 가 나옴
```

- 크롬 브라우져에서 개발자 도구 실행 시 node.js 아이콘 생김 -> 클릭

```javascript
node --inspect-brk 파일명
// 실행 시 파일 첫줄에 break point 걸린 효과가 나타남 -> 개발자 도구에서 확인 가능
```

- 위 명령어들은 nodemon으로도 실행 가능

### **2. VS code로 node.js 디버깅하기**

- node.js파일에서 특정라인 브레이크포인트 지정
- vs code에서 디버그 탭 접속
- 좌 상단 실행아이콘 선택 -> 가운데 상단 node.js 선택
- 변수 추적은 좌측 상단에서 확인 가능

```javascript
node --inspect 파일명
// 실행 시 debugging listening on '주소' 가 나옴
```
