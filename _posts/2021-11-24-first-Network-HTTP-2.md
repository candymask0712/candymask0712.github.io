---
title: "[Network] HTTP/네트워크 기초 - 2 (브라우저 작동원리 - 상)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Network
tags:
  - HTTP
  - URI
  - URL
  - IP
  - DNS
  - Domain

last_modified_at:
---

### **1. URL과 URI**

1. URL

   - Uniform Resource Locator의 약자, 네트워크에서 리소스 파일의 위치 정보 나타냄
   - URL은 scheme, hosts, url-path로 구성

2. URI

   - Uniform Resource Identifier의 약자, URL을 포함하는 상위 개념
   - URL의 기본 요소인 scheme, hosts, url-path에 query, bookmark를 포함

     | 명칭     | 설명                               | 예시                             |
     | -------- | ---------------------------------- | -------------------------------- |
     | scheme   | 통신 프로토콜                      | file://, https://                |
     | hosts    | 리소스가 위치한 웹서버, 도메인, IP | 127.0.0.1, www.google.com        |
     | port     | 웹 서버에 접속하기 위한 통화       | :80, :443, :3000                 |
     | url-path | 웹 서버의 루트부터 파일까지의 경로 | /search, /Users/username/Desktop |
     | query    | 웹 서버에 전달하는 추가 질문       | q=JavaScript                     |

### **2. IP와 PORT**

1. IP Address

   - Internet Protocol address의 약자, 흔히 IP주소라고 부름
   - 네트워크에 연결 된 특정 PC의 주소를 나타내는 체계
   - localhost, 127.0.0.1 : 현재 사용 중인 로컬 PC
   - 0.0.0.0, 255.255.255.255 : 로컬 네트워크에 접속된 모든 장치와 소통하는 주소
   - broadcast address이며 접근가능한 IP로 지정 시 모든 기기에서 서버에 접속 가능
   - IPv4 (IP version 4) 2^32개(약 43억 개) 주소 할당 가능 -> 한계 도달
   - IPv6 (IP version 6) 2^128개 주소 할당 가능 (현재 IPv4와 병행 사용 중)

2. PORT

   - IP주소가 가리키는 PC에 접속 할 수 있는 통로(채널)
   - 포트번호는 0 ~ 65,535까지 사용 가능 (0~1024번은 통신규약에 따라 정해짐)
   - 주요 포트 번호 : 22(SSH), 80(HTTP), 443(HTTPS)

### **3. 도메인과 DNS**

1. 도메인

   - 특정 사이트 접속 시 IP주소를 대신하여 사용하는 주소
   - IP주소가 도로명 주소라면 도메인은 상호명 역할(짧고 직관적으로 위치 파악 가능)

2. DNS

   - Domain Name System의 약자, 도메인/IP주소 변환을 위한 데이터베이스 시스템
   - 호스트의 도메인 <---- 변환 -----> IP주소
   - 주소창에 naver.com 입력 시 브라우져는 DNS에서 IP 주소(125.209.222.142) 찾음
