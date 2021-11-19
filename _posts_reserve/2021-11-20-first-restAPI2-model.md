---
title: "[Network] 좋은 REST API를 디자인하는 방법 (성숙도 모델)"
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

## **1. REST API**

- REST : Representational State Transfer 의 약자
- REST API : 웹에서 사용하는 데이터를 HTTP URI로 표현하고 HTTP 프로토콜을 통해 요청과 응답을 정의하는 방식

## **2. REST 성숙도 모델**

- REST API를 잘 적용하기 위해 리차드슨이 만든 4단계 모델 (0 ~ 3단계)
- 3단계까지 지키기 어렵기 때문에 2단계까지만 지켜도 좋은 디자인이고 HTTP API라고 부름

### \*_3. 단계별 성숙도 모델_

- 0단계

  - 단순히 HTTP 프로토콜을 사용 (REST API는 아님)
  - 좋은 REST API를 작성하기 위한 기본 단계

- 1단계

  - 모든 자원은 개별 리소스에 맞는 엔드포인트 사용
  - 요청하고 받은 자원에 대한 정보를 응답으로 전달

- 2단계

  - CRUD에 맞게 적절한 HTTP 메소드를 사용
  - 응답코드를 명확히 작성 및 관련 리소시를 Location헤더에 작성된 URI를 통해 확인할 수 있어야 함

- 3단계

  - 하이퍼미디어컨트롤 적용(HATEOAS)
  - 요청은 2단계와 동일
  - 응답에서는 2단계와 달리 리소스의 URI를 포함한 링크 요소를 삽입하여 작성

[참고자료- Richardson 성숙도 모델](https://brunch.co.kr/@pubjinson/12)
