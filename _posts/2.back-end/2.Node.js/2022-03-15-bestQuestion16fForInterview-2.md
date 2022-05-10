---
title: "[JS] Node.js의 주요 특징"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Node.js
tags:
  - interview

last_modified_at:
---

### **1. Node.js 관련 질문**

1. Node.js는 싱글스레드인가요. Node.js 런타임이 동작하는 방식

   - Node.js 싱글스레드 기반으로 작동
   - 그러나 Non-blocking I/O와 이벤트 루프를 통해 효과적 처리 가능

   참고자료

   [[[Node.js] Node.js는 싱글 스레드?]](https://velog.io/@daeseongkim/Node.js-Node.js%EB%8A%94-%EC%8B%B1%EA%B8%80-%EC%8A%A4%EB%A0%88%EB%93%9C)

2. Node.js 에서 비동기의 개념은 어떻게 되나요?

   - 비동기 요청 발생 시 Event Loop가 처리
   - 처리하는 동안 제어권은 다음 요청으로 넘어감
   - 처리가 완료되면 Callback을 사용 호출 측에 그 사실을 알려줌

   참고자료

   [[NodeJS에서 비동기의 개념에 대해서]](https://velog.io/@nain93/NodeJS%EC%97%90%EC%84%9C-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%9D%98-%EA%B0%9C%EB%85%90%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)

   [[Node.js: 비동기 프로그래밍 이해]](https://www.nextree.co.kr/p7292/#:~:text=Node.js%20%EC%9D%98%20%EB%B9%84%EB%8F%99%EA%B8%B0%20%EC%B2%98%EB%A6%AC%EB%8A%94%20%EC%9D%B4%EB%B2%A4%ED%8A%B8%20%EB%B0%A9%EC%8B%9D%EC%9C%BC%EB%A1%9C%20%ED%92%80%EC%96%B4,Event%20Loop%EA%B0%80%20%EC%B2%98%EB%A6%AC%ED%95%A9%EB%8B%88%EB%8B%A4.)

3. Node.js와 웹 브라우저의 차이점에 대해서 설명해주세요

   |            | 내용                                                                 |
   | ---------- | -------------------------------------------------------------------- |
   | 공통점     | JS기반(엔진 내장)                                                    |
   | 차이점     | 환경별 API 차이, 모듈 키워드 차이                                    |
   | Node.js    | 크롬 V8 엔진 기반, 웹페이지 랜딩 목적, 버전 선택 가능, CommonJS 모듈 |
   | 웹브라우저 | 엔진 종류 다양, 서버 개발 환경이 주 목적, ES 표준 모듈               |

   참고자료

   [[node.js와 브라우저의 차이점]](https://velog.io/@shitaikoto/Node.js-browser#:~:text=node.js%EC%99%80%20%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98%20%EC%B0%A8%EC%9D%B4%EC%A0%90,-node.js%EC%99%80&text=Node.js%EB%8A%94%20V8%20%EC%97%94%EC%A7%84,%EC%A0%9C%EA%B3%B5%ED%95%98%EB%8A%94%20%EA%B2%83%EC%9D%B4%20%EB%AA%A9%EC%A0%81%EC%9D%B4%EB%8B%A4.)

   [[Node.js와 브라우저의 차이]](https://velog.io/@shitaikoto/Node.js-browser#:~:text=node.js%EC%99%80%20%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98%20%EC%B0%A8%EC%9D%B4%EC%A0%90,-node.js%EC%99%80&text=Node.js%EB%8A%94%20V8%20%EC%97%94%EC%A7%84,%EC%A0%9C%EA%B3%B5%ED%95%98%EB%8A%94%20%EA%B2%83%EC%9D%B4%20%EB%AA%A9%EC%A0%81%EC%9D%B4%EB%8B%A4.)
