---
title: "[Network] HTTP/네트워크 기초 - 4 (HTTP 요청과 메세지)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Network
tags:
  - HTTP

last_modified_at:
---

### **1. HTTP**

- HyperText Transfer Protocol의 약자
- HTML과 같은 문서를 전송하기 위한 Application Layer 프로토콜
- 가장 큰 특징은 'Stateless(무상태성)'
- 서버 통신과정에서 HTTP는 상태 저장 안함 -> 쿠키, 세션 등을 통해 처리

### **2. HTTP messages**

- HTTP messages 는 클라이언트와-서버 데이터 교환 방식
- 요청과 응답은 다음과 같은 유사한 구조를 가집니다.
  - start line : 요청/응답의 상태, 항상 첫 줄에 위치 (응답에서는 status line)
  - HTTP headers : 요청을 지정 OR 메시지 본문을 설명하는 헤더의 집합
  - empty line : 헤더와 본문을 구분하는 빈 줄
  - body : 요청/응답과 관련된 데이터 또는 문서를 포함 (유형에 따라 선택적으로 사용)

1. 요청(Requests)

   - Start line

     - HTTP method (수행할 작업을 설명)
     - 요청 대상 (일반적으로 URL이나 URI 또는 프로토콜)
     - HTTP 버전 (버전에 따라 HTTP message의 구조가 달라짐)

   - Headers

     - Request headers : 가져올 리소스나 클라이언트 자체에 대한 자세한 정보를 포함
     - General headers : 메시지 전체에 적용, body 부분과는 관련 X
     - Representation headers : body에 담긴 리소스의 정보(컨텐츠 길이, MIME 타입 등)를 포함

   - Body
     - 마지막에 위치 / POST나 PUT등에서 데이터 업뎃을 위해 사용
     - Single-resource bodies(단일-리소스 본문) : 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성
     - Multiple-resource bodies(다중-리소스 본문) : 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지님

2. 요청(Responses)

   - Start line

     - 현재 프로토콜의 버전(HTTP/1.1)
     - 상태 코드 - 요청의 결과를 나타냄
     - 상태 텍스트 - 상태 코드에 대한 설명

   - Headers

     - Response headers : 응답 관련 부가정보 (위치 또는 서버 정보(이름, 버전 등))
     - General headers : 메시지 전체에 적용, body 부분과는 관련 X
     - Representation headers : body에 담긴 리소스의 정보(컨텐츠 길이, MIME 타입 등)를 포함

   - Body
     - 마지막에 위치 / 201, 204 등의 상태 코드 응답에는 본문 필요 X
     - Single-resource bodies(단일-리소스 본문) : 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성
     - 길이를 모를 경우 Transfer-Encoding이 chunked 로 설정되어 있으며, 파일은 chunk로 나뉘어 인코딩되어 있습니다.
     - Multiple-resource bodies(다중-리소스 본문) : 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지닙
