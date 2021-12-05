---
title: "[TypeScript] 컴파일 세부설정 (tsconfig.json)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - TypeScript
tags:
  - JavaScript
last_modified_at:
---

### **1. 컴파일 세부설정**

- tsconfig.json 생성
- TS파일을 JS파일로 변환 시의 세부설정 가능

### **2. 기본 옵션**

- 기본적인 옵션 설정

  ```typescript
    {
    "compilerOptions": {
        "target": "es5",
        // 어떤 버젼의 js로 바꿔줄지 결정
        "module": "commonjs",
        // import 시 어떤 문법을 쓸지
        // commonjs(require), es5~(import)
        "noImplicitAny": true,
        // any 타입이 의도치 않게 발생시 에러 알림
        "strictNullChecks": true
        // null, undefined 타입에 조작시 에러 알림
        }
    }
  ```

### **3. 주요 옵션**

- 기본적인 옵션 설정

  ```typescript
    {
    "compilerOptions": {

      "target": "es5", // 'es3', 'es5', 'es2015', 'es2016', 'es2017','es2018', 'esnext' 가능
      "module": "commonjs", //무슨 import 문법 쓸건지 'commonjs', 'amd', 'es2015', 'esnext'
      "allowJs": true, // js 파일들 ts에서 import해서 쓸 수 있는지
      "checkJs": true, // 일반 js 파일에서도 에러체크 여부
      "jsx": "preserve", // tsx 파일을 jsx로 어떻게 컴파일할 것인지 'preserve', 'react-native', 'react'
      "declaration": true, //컴파일시 .d.ts 파일도 자동으로 함께생성 (현재쓰는 모든 타입이 정의된 파일)
      "outFile": "./", //모든 ts파일을 js파일 하나로 컴파일해줌 (module이 none, amd, system일 때만 가능)
      "outDir": "./", //js파일 아웃풋 경로바꾸기
      "rootDir": "./", //루트경로 바꾸기 (js 파일 아웃풋 경로에 영향줌)
      "removeComments": true, //컴파일시 주석제거

      "strict": true, //strict 관련, noimplicit 관련 모드 전부 켜기
      "noImplicitAny": true, //any타입 금지 여부
      "strictNullChecks": true, //null, undefined 타입에 이상한 짓 할시 에러
      "strictFunctionTypes": true, //함수파라미터 타입체크 강하게
      "strictPropertyInitialization": true, //class constructor 작성시 타입체크 강하게
      "noImplicitThis": true, //this 키워드가 any 타입일 경우 에러
      "alwaysStrict": true, //자바스크립트 "use strict" 모드 켜기

      "noUnusedLocals": true, //쓰지않는 지역변수 있으면 에러
      "noUnusedParameters": true, //쓰지않는 파라미터 있으면 에러
      "noImplicitReturns": true, //함수에서 return 빼먹으면 에러
      "noFallthroughCasesInSwitch": true, //switch문 이상하면 에러
    }
  }
  ```

[참고자료 - codingapple TS 강의](https://codingapple.com/course/typescript-crash-course/)
[전체 세팅 항목](https://www.typescriptlang.org/tsconfig)
