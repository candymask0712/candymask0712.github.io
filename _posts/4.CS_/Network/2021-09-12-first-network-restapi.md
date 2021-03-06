---
title: "[Network] REST API란"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Network
tags:
  - REST API
  - JavaScript
last_modified_at:
---

## **1. API**

- Application Progamming Interface의 약자
- 프로그램 간 통신을 위한 규약
- (웹 개발 시)서버와 클라이언트 간 통신 규약

## **2. REST API**

- 좋은 API 작성을 위한 규칙
- 웹 태동기에 Roy Fielding이 제안한 6가지 규칙
- 요청만 보고도 요청의 의도 파악 가능

## **3. REST의 원칙 6가지**

- 위 쪽에 있는 1 ~ 3번이 특히 중요한 원칙

### **1. Uniform Interface**

- 하나의 자료는 하나의 URL로
- URL 하나를 알면 둘을 알수 잇어야함
- 요청과 응답은 정보가 충분히 들어있어야 함

### **2. client-server 구조**

- 브라우저는 요청만, 서버는 응답만 해야함

### **3. Stateless(무상태성)**

- 요청1과 요청2는 의존성이 없어야 함

### **4. Cacheable(캐시가능)**

- 서버에서 보내는 정보는 캐싱이 가능해야 함
- 캐싱을 위한 버전도 잘 관리해야 함

### **5. Layered System(계층형 구조)**

- REST 서버는 다중 계층으로 구성 될 수 있음

### **6. Code on Demand**

- Rest API 메세지만 보고 쉽게 이해할 수 있는 구조

## **3. REST API의 주요 이름짓기 원칙**

- URL은 되도록 명사로 작성
- 하위문서 나타낼 시 확장자 쓰지 않기
- 띄어쓰기는 대시(-)를 이용
- 자료하나 당 하나의 URL를 사용

[참고자료-얄팍한 코딩사전](https://www.youtube.com/watch?v=iOueE9AXDQQ)  
[참고자료-코딩애플](https://codingapple.com/course-status/)
