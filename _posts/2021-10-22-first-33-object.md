---
title: "[JS] 객체의 이해 및 메서드"
excerpt: "21년 10월 22일 공부일지 "
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - JS
  - TIL
last_modified_at:
---

### **1.객체란**
- 여러 속성을 하나의 변수에 저장하는 데이터 타입
- key/value pair가 property를 구성하고, comma로 구분
- 객체 변수를 복사 시 reference가 복사 됨

### **2.객체의 사용**

- Dot notation: `객체명.변수명` 의 형태로 사용
- Braket notation: `객체명[변수명]`의 형태로 사용
```javascript
const obj = { name: james }
obj.name // 결과값 : james
obj['name'] // 결과값 : james
obj[name] // 만약 name이 동적변수인 경우
```

### **3.객체 값 추가/삭제/포함여부**

1. 추가
- Dot notation: `객체명.변수명 = 값` 의 형태로 사용
- Braket notation: `객체명[변수명] = 값`의 형태로 사용
   ```javascript
   const obj = { name: james }
   obj.name = john // obj가 { name: john } 으로 변경
   obj['name'] // obj기 { name: john } 으로 변경
   ```

2. 삭제
- 객체 값 조회 앞에 `delete`를 사용해 삭제
   ```javascript
   const obj = { name: james }
   delete obj.name = john // obj가 {} 으로 변경
   delete obj['name'] = john // obj가 {} 으로 변경   
   ```

2. 삭제
- 객체 값 조회 앞에 `delete`를 사용해 삭제
   ```javascript
   const obj = { name: james }
   delete obj.name = john // obj가 {} 으로 변경
   delete obj['name'] = john // obj가 {} 으로 변경   
   ```

3. 포함 여부 확인
- `'key값' in 객체명`의 형태로 확인 가능(T/F 반환)
   ```javascript
   const obj = { name: james }
   name in obj // true
   age in obj // false
   ```

- 단, `key in~` 방식은 프로토타입 체인으로 생성한 프로파티도 체크하여 T/F 반환  
- `객체명.hasOwnProperty('key값')` 사용으로 커버가능
- 객체가 키를 직접속성으로 포함하는지 여부 반환
   ```javascript
   const obj = {
	   a:'1'
      }
      Object.prototype.b= undefined

      console.log( obj.hasOwnProperty('a') ) // true
      console.log( obj.hasOwnProperty('b') ) // false
   ```

[참고자료 - key in과 hasOwnProperty의 차이](https://velog.io/@minong/Javascript-%EA%B0%9D%EC%B2%B4%EC%97%90-%ED%95%B4%EB%8B%B9-key%EA%B0%92%EC%9D%B4-%EC%A1%B4%EC%9E%AC%ED%95%98%EB%8A%94%EC%A7%80-%ED%99%95%EC%9D%B8%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

