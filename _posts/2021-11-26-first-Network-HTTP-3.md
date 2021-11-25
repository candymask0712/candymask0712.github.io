---
title: "[Network] HTTP/네트워크 기초 - 3 (브라우저의 작동원리 - 하)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Network
tags:
  - HTTP
  - AJAX
  - SSR
  - CSR
  - CORS

last_modified_at:
---

https://urclass.codestates.com/8b42cac5-a994-411f-bcb8-73c41c582ef0?playlist=549

### **1. AJAX**

- Asynchronous JavaScript And XMLHttpRequest의 약자
- JavaScript, DOM, Fetch, XMLHttpReqest, HTML 등 사용하는 웹 개발 기법
- 웹 페이지에 필요한 부분에 필요한 데이터만 받아 비동적으로 화면에 그림
- fetch를 이용해 페이지 이동없이 데이터 받고 DOM에 적용시켜 구현

1. AJAX의 장점

   - 서버에서 HTML을 완성해 보내지 않아도 필요한 데이터만 받아와 랜더링 가능
   - XHR이 표준화 되어 브라우저 무관 AJAX 사용 가능
   - 빠르고 더 많은 상호 작용 가능 -> 더 나은 유저 경험
   - 필요한 데이터를 텍스트 형태로 보냄 -> 더 작은 대역폭으로도 가능

2. AJAX의 단점

   - SEO에 불리 (처음받는 HTML파일에는 데이터를 채우기위한 틀만 존재)
   - 뒤로가기 버튼 : AJAX에서는 이전 상태 기억X (별도 History API 필요)
   - 빠르고 더 많은 상호 작용 가능 -> 더 나은 유저 경험
   - 필요한 데이터를 텍스트 형태로 보냄 -> 더 작은 대역폭으로도 가능

### **2. SSR vs CSR**

1. SSR

   - Server Side Rendering의 약자, 웹페이지를 서버에서 랜더링
   - SEO가 중요 / 첫 화면의 빠른 렌더링 / 사용자와 상호작용 적은 경우 사용

2. CSR

   - Client Side Rendering의 약자, 웹페이지를 클라이언트에서 랜더링
   - SEO가 중요 X / 빠른 라우팅 -> 강력한 사용자 경험 / 빠른 동적 렌더링 -> 좋은 사용자 경험

### **3. CORS**

- Cross-Origin Resource Sharing의 약자
- 처음 전송되는 리소스의 도메인과 다른 도메인으로부터 리소스가 요청 될 경우 발생(AJAX 요청일 때만)
- SOP, Same Origin Policy에 의해 기본적으로는 막혀 있음
- 프로토콜 - 호스트(도메인) - 포트번호가 모두 같아야 같은 Origin임
- CORS가 허용 될 경우 보안에 위협이 될 수 있어서 유의해야 함
- simple requset(조건 충족 시) 외에는 preflight 요청을 먼저보내 안전여부 확인

[참고자료 - 지메일이 핫메일을 이긴 진짜 이유](https://sungmooncho.com/2012/12/04/gmail-and-ajax/)
