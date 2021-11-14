---
title: "[React] 기본 CRUD구현 (state, props)"
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - state
  - props
last_modified_at:
---

### **Web-app의 장점**

1. 모바일앱으로 발행이 쉬움
2. 앱처럼 뛰어난 UX (사용성, 속도)
3. 좋은 UX가 비지니스적 강점(구매율 등)

### **React 프로젝트 시작**

```javascript
$ yarn create react-app 프로젝트명
$ cd 프로젝트명
$ yarn start
```

### **블로그 기본 CRUD구현 (state, props)**

#### 1. 읽기(Read)

1. 기본리스트

- 배열로 기본 리스트 생성 후 useState로 관리
- Map으로 리스트를 하단에 노출

2. 모달창에 노출하기 (props)

- app 매서드 밖에 Modal 매서드 생성(대문자 시작)
- app 에서 <Modal 보낼이름={보낼변수명}> 형식으로 props 보냄
- Modal 매서드에서 props값 받음 (비구조화할당 사용 시 편함)

```javascript
const Modal = (props) => {
  const = [보낼이름] = props;
  return (
    <>
      <h2>{props.보낼이름}</h2>
    </>
  )
}
// props 기본 사용법
```

```javascript
const Modal = (props) => {
  const = [보낼이름1, 보낼이름2] = props;
  return (
    <>
      <h2>{보낼이름1}</h2>
      <h2>{보낼이름2}</h2>
    </>
  )
}
//props를 여러 개 보낼 때 비구조화 할당 사용
```

```javascript
const Modal = ({ 보낼이름 }) => {
  return (
    <>
      <h2>{보낼이름}</h2>
    </>
  );
};
// 비구조화할당을 함수의 파라미터 부분에서 사용
```

#### 2. 생성(Create)

- 새로 생성되는 input을 useState로 관리
- onChange 사용 input을 업데이트(세터함수 필수)

#### 3. 갱신(Update)

- onClick 사용 생성된 input을 리스트에 추가
  1. 추가 시 spread 문법 사용 deep copy
  2. copy한 배열에 unshift로 추가

#### 4. 삭제(Delete)

- onClick 사용 삭제할 글의 id를 삭제함수로 전달
- 삭제함수에서 filter 이용 해당글 제외한 새 배열 생성

#### 5. 기타 테크닉 (편의성)

- onKeyPress 사용 시 엔터로 편하게 추가가능

```javascript
함수명 = (e) => {
  if(e.key === 'Enter') {
    클릭시 실행 할 함수
  }
}
// 위와 같이 작성 시 Enter로도 클릭과 같은효과
// 인자가 e.key이고 'Enter'가 대문자 및 String 타입임에 주의
```

- useRef 사용 시 추가 후 input으로 커서 이동 가능

```javascript
const 변수명 = useRef(null); // useRef 이용 생성
변수명.current.focus() // 작동 원하는 매서드에 삽입
<... ref={변수명}> // 원하는 커서 위치 태그에 삽입
```

#### 6. 주의사항

- 인자를 포함한 함수 실행시 화살표함수 형태로 작성

```javascript
onClick={DeleteContent(x.id)} // 작동하지 않음
onClick={()=>DeleteContent(x.id)} // 작동
```

- 만약 화살표함수 없이 실행을 원할 시 아래와 같이 작성

```javascript
const 함수명 = (인자) => {}; // 기존 내용
const 함수명 = (인자) => () => {}; // 왼쪽처럼 수정시 바로 실행
```

관련 링크 : https://okky.kr/article/1065642?note=2532968
