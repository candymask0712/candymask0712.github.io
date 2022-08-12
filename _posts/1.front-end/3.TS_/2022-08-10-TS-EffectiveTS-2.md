---
title: "[TypeScript] Effective TS - item.02 - TS 설정 이해"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - Effective TS
  - tsconfig
last_modified_at:
---

### **1. TS의 설정을 담당하는 tsconfig.json**

- TS의 설정은 소소 파일 위치와 출력 제어가 대부분
- 그러나, 언어 자체의 핵심 요소를 제어하는 설정도 존재
- strict 설정 시 두 개의 핵심 설정 사용 가능 (noImplicitAny, strictNullChecks)

### **2. 핵심 설정 (1) - noImplicitAny**

- 암시적으로 any로 간주 되는 타입을 금지
- 의도치 않게 any를 사용하는 경우를 막아 타입 안정성 확보

```TypeScript
// parameter인 a는 암묵적으로 any 타입을 가짐
const func = (a) => a
// noImplicitAny: true 설정 시 a에 반드시 타입을 설정해야함
const func = (a: number) => a
```

### **2. 핵심 설정 (2) - strictNullChecks**

- null과 undefined을 모든 타입에서 허용할지 여부 결정
- 두 값을 명시적으로 허용해야 되 코드작성을 어렵게 하지만
- 'undefined는 객체가 아닙니다' 같은 런타임 오류 예방에 좋음

```TypeScript
// trictNullChecks: false 인 경우
// number 타입으로 설정했으나 null 값도 허용함
const x: number = null

// trictNullChecks: true 인 경우
// null 값은 명시적으로 허용해야만 할당 가능
const x: number | null = null
```
