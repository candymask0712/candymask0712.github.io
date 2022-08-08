---
title: "[TypeScript] Udemy 강의 - 1 ~ 20 (TS vs JS, enum) "
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - String literal
  - Comong
last_modified_at:
---

### **1. TS vs JS Type**

- JS에서도 별도 코드 작성 시 타입체크 가능 (아래 예시)
- 하지만 JS는 런타임 단계에서만 타입체크 가능
- 그러나 TS는 컴파일 단계에서 체크 가능한 장점(개발 단계에서 발견)

```JavaScript
function Test(n1: number, n2:number) {
  if(typeof n1 !== 'number' ||typeof n2 !== 'number')  {
    throw new Error('Incorrect Input')
  }
}

```

### 2. enum의 활용

- 자동적으로 전역에서 상수 식별자를 붙여줌
- 값을 인간이 읽을 수 있고 백그라운드에서 매핑된 값이 존재

```JavaScript

// 역할 등 부여 시 글자 구분자는 표현/문법 차이가 헷갈리게 함
const role = 'read'
const role = 'read only'
const role = 'read-only'
const role = 'read_only'

// 역할 등의 부여를 위해 숫자를 할당
let admin = 0;
let user = 1;
let vip = 2;

// 숫자로 된 구분자는 기억에 의존해야 되고 헷갈릴 수 있음
const person = {
  name: kim,
  role: 1
}

// enum 사용 시 간편하게 관리 가능
enum Role { admin, read_only, vip }
// Role.admin = 0
// Role.read_only = 1
// Role.vip = 2

// 넘버링의 시작을 바꿀 수 있음
enum Role { admin = 1, read_only, vip }
// Role.admin = 1
// Role.read_only = 2
// Role.vip = 3

// 요소마다 임의의 넘버링을 부여할 수도 있음 (+문자할당 가능)
enum Role { admin = 5, read_only = 100, vip = 'yeah' }
// Role.admin = 5
// Role.read_only = 100
// Role.vip = 'yeah'

```
