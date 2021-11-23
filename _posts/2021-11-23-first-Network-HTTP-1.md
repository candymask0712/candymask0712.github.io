---
title: "[Network] HTTP/네트워크 기초 - 1 (클라이언트-서버 아키텍처)"
excerpt: "21년 월 일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Network
tags:
  - HTTP
last_modified_at:
---

### **1. 클라이언트-서버 아키텍처**

1. 클라이언트-서버 아키텍처(2-Tier Architecture)

   - 만약 앱 내 모든 정보를 앱 자체에 저장한다면 -> 내용바뀔 때마다 업데이트 필요
   - 2-Tier 아키텍처 : 리소스 존재하는 곳(서버)과 리소스를 사용하는 곳(앱)을 분리
   - 3-Tier 아키텍처 : 서버는 리소를 전달할 뿐 리소스는 데이터베이스에 저장

2. 클라이언트 서버 통신과 API

   - 프로토콜 : 서버-클라이언트 통신을 위한 통신 규약
   - 웹 어플리케이션에서는 HTTP 프로토콜을 이용해 통신
   - API : Application Programming Interface
   - 서버가 클라이언트에게 리소스를 잘 활용할 수 있도록 인터페이스 제공
   - 클라이언트가 적절한 요청을 할 수 있도록 일종의 메뉴판 제공
   - 보통 인터넷에 있는 데이터 전달은 주소(URI, URL)을 통해 접근

   - 요청 종류별 주요 메서드

   | 요청         | 메서드    |
   | ------------ | --------- |
   | 조회(read)   | GET       |
   | 추가(create) | POST      |
   | 갱신(update) | PUT/PATCH |
   | 삭제(date)   | DELETE    |
