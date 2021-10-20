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

```javascript
```
`<code>` 코드강조

[링크명](링크주소)    
![대체텍스트](이미지주소)

*** 
수평선

>인용
>>인용2

| | |
---|---
| | |
| | |

| | |
---|---
| 
|

<small></small>