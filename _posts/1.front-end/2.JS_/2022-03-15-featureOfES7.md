---
title: "[JS] JavaScript의 주요 특징"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - interview

last_modified_at:
---

### **1. JavaScript 관련 질문**

1. var, let, const의 차이점과 호이스팅 (Hoisting)

   - var, let, const은 재선언 및 재할당 여부 차이

     |       | 재선언 | 재할당 |
     | ----- | ------ | ------ |
     | var   | O      | O      |
     | let   | X      | O      |
     | const | X      | X      |

   - 호이스팅 : 코드 실행 전 변수/함수선언이 스코프 최상단으로 끌어올려 진듯한 현상

2. Javascript와 Nodejs의 차이점

   - JS : 브라우저에서 클라이언트 랜더링 시 사용
   - node : 브라우저 환경 외에도 크롬 v8 사용 JS활용(서버 등)  
     [Javascript와 Nodejs가 어떻게 다른 것인지 설명해주세요.](https://velog.io/@bleach7/Javascript%EC%99%80-Nodejs%EA%B0%80-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%8B%A4%EB%A5%B8-%EA%B2%83%EC%9D%B8%EC%A7%80-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94#:~:text=nodejs%EB%A5%BC%20%ED%86%B5%ED%95%98%EC%97%AC%20%ED%8A%B9%EC%A0%95%ED%95%9C%20%ED%99%98%EA%B2%BD,%EA%B2%83%EC%9D%B4%20%EB%B0%94%EB%A1%9C%20Node.js%EC%9D%B4%EB%8B%A4.)

3. 모든 JS 파일을 브라우저에서 한 번에 로딩 시 문제점

   - JS파일을 불러오는 동안 HTML 구문분석을 중단
   - 스크립트 파일 로드 되는 동안 화면 중단(이탈, 새로고침)  
     [[번역]How to load JavaScript properly](https://bedeveloper.tistory.com/89)  
      [[JS]모든 자바스크립트 파일을 브라우저에서 한 번에 로딩 할 때의 문제점](https://velog.io/@juunghunz/JS%EB%AA%A8%EB%93%A0-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90%EC%84%9C-%ED%95%9C-%EB%B2%88%EC%97%90-%EB%A1%9C%EB%94%A9-%ED%95%A0-%EB%95%8C%EC%9D%98-%EB%AC%B8%EC%A0%9C%EC%A0%90%EC%9D%84-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94#:~:text=%EB%B6%84%EC%84%9D%EC%9D%84%20%EC%A4%91%EB%8B%A8-,%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%8C%8C%EC%9D%BC%EC%9D%80%20%ED%95%B4%EB%8B%B9%20%ED%8C%8C%EC%9D%BC%EC%9D%84%20%EA%B0%80%EC%A0%B8%EC%98%AC%20%EB%95%8C%EA%B9%8C%EC%A7%80,%EC%8B%9C%EA%B0%84%EC%9D%B4%20%EA%B8%B8%EC%96%B4%EC%A7%80%EA%B2%8C%20%EB%90%9C%EB%8B%A4.&text=%EC%83%88%EB%A1%9C%EA%B3%A0%EC%B9%A8%EC%9D%84%20%EA%B3%84%EC%86%8D%ED%95%98%EA%B2%8C,%EC%9D%B4%20%EC%A6%9D%EA%B0%80%ED%95%A0%EC%88%98%20%EC%9E%88%EA%B2%8C%20%EB%90%9C%EB%8B%A4.)

4. Promise의 개념과 콜백 함수의 차이점

   - promise : 자바스크립트 비동기 처리에 사용되는 객체 (서버통신 시 주로 사용)
   - 콜백함수는 연속적인 비동기 패턴 사용 시 코드 복잡해짐  
     [[TIL] promise의 개념과 콜백 함수 방식과의 차이점](https://velog.io/@steel_hyuk___2/promise%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98-%EB%B0%A9%EC%8B%9D%EA%B3%BC%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
