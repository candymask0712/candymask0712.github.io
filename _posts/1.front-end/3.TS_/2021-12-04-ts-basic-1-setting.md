---
title: "[TypeScript] TS 사용이유와 기본 셋팅&사용법"
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

### **1. TS를 쓰는 이유 (엄격한 타입체크)**

- TS는 Dynamic Typing 없음 (예상못한 부작용 방지)

  ```javascript
  let a = 5 - "3"; // 2 (JS는 타입 자동변환)
  ```

- TS는 에러메세지가 비교적 정확 (엄격한 타입체크)

### **2. 기본셋팅 (React)**

1. 기존 프로젝트에 설치

   ```bash
   npm install --save typescript @types/node @types/react @types/react-dom @types/jest
   // yarn add로도 가능
   ```

2. 프로젝트 새로 생성

   ```bash
   npx create-react-app my-app --template typescript
   // yarn add로도 가능
   ```

### **3. 기본 사용법**

1. 변수 선언시 타입 지정

   - 타입 지정 시 변경 불가

     ```typescript
     let 이름: string = "kim"; // 이름 변수에는 string만 가능
     이름 = 123; // 에러 발생
     ```

   - 변수 타입 지정

     ```typescript
     let 이름: string = "kim"; // 변수 타입 다양하게 지정
     // string, number, boolean, null, undefined, biginit 등

     let 이름: string[] = ["kim", "park"]; // 배열의 지정
     // 배열 안에 String타입의 요소만 들어올 수 있음

     let 이름: { name: string } = { name: "kim" }; // 객체의 지정
     // 값으로 String타입만 들어올 수 있음
     let 이름: { name?: string } = { name: "kim" };
     // name 속성은 옵션
     ```

   - 다양한 변수 들어올 수 있게 타입 지정

     ```typescript
     let 이름: string | number = "kim"; // union 타입
     // string, number 타입이 들어올 수 있음
     ```

   - 타입을 변수에 담아 사용 가능(Type alias)

     ```typescript
     type Name = string | number;
     let 이름: Name = "kim";
     // Type alias는 차별화를 위해 대문자로 보통 시작
     ```

2. 함수에 타입 지정

   - 함수는 파라미터와 리턴값 각각에 타입지정 가능

   ```typescript
   function 함수(x: number): number {
     return x * 2;
     // 파라미터로 숫자, 리턴값에 숫자가 들어는 함수
   }
   ```

3. 배열에 적용하는 tuple 타입이

   - 함수는 파라미터와 리턴값 각각에 타입지정 가능

   ```typescript
   type Member = [number, boolean];
   // 무조건 첫째는 숫자, 둘째는 불리언 값이 와야함
   let join: Member = [];
   ```

4. 객체에 들어갈 키 값이 여러 개라면

   - 함수는 파라미터와 리턴값 각각에 타입지정 가능

   ```typescript
   type Member = {
     name: string;
   };
   // 키 값으로는 name만, value로는 문자만 가능

   type Member = {
     [key: string]: string;
   };
   // 속성의 키 값으로는 문자, 값으로도 문자만 가능
   ```

5. 클래스의 타입 지정

   ```typescript
   class User {
     name: string;
     constructor(name: string) {
       this.name = name;
     }
   }
   ```

[참고자료 - codingapple TS 강의](https://codingapple.com/course/typescript-crash-course/)
