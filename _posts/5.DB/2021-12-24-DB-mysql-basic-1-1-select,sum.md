---
title: "[DB] SQL의 기본문법 - 1 - SELECT"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - MySQL
tags:
  - SELECT
  - MySQL
last_modified_at:
---

### **1. SELECT**

- 정렬하기

```sql
SELECT NAME, DATETIME FROM ANIMAL_INS ORDER BY ANIMAL_ID DESC
-- ASC는 오름차순 DESC는 내림차순 (ASC가 기본값)

SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION="Sick" ORDER BY ANIMAL_ID, NAME
-- 여러 조건으로 정렬할 시 콤마로 조건 추가
```

- 조건 특정하기

```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION="Sick" ORDER BY ANIMAL_ID
-- WHERE 뒤에 원하는 조건 작성

```

- 상위 n개 추출하기

```sql
SELECT name FROM animal_ins ORDER BY datetime LIMIT 1  
-- limit를 사용하면 상위 n개 추출
-- limit 2,6처럼 표현하면 상위 2위~ 6위까지

```
