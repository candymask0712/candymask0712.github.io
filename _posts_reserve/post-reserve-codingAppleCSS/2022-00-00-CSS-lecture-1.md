---
title: "[CSS] HTML/CSS - 1 - 웹페이지 레이아웃 만들기 "
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - Algorithm
  - React
  - JS
  - TIL
last_modified_at:
---

### **1. 레이아웃 만들기 1 : 호환성 좋은 float**

- 이미지 정렬 시

```CSS
display : block;
margin-left : auto;
margin-right : auto;
```

- 텍스트의 일부만 스타일 변경 시 => <span> 태그 사용
- <span> 태그는 display:inline 속성을 내포(폭, 높이 단독적용 불가)

```JS
<p>안녕하세요 저는 <span style="color : red;">노력하는</span> 개발자입니다.</p>
```

[참고자료 = display : block, inline의 차이](https://seungwoohong.tistory.com/23)

### **2. div를 이용한 박스 디자인**

1. div태그에 많이 적용하는 기본 옵션

- 모든 div, p, h1, li 등은 display : block 내장
- 그냥 사용 시 한 행을 전부 차지 => display 옵션 수정 변경 필요

```CSS
.box {
  margin : 20px;
  padding : 30px;
  border : 1px solid black;
  border-radius : 5px;
}
```

2. 일부 스타일은 inherit 됨

- font-size, color, font-family, text-align 이런 속성들은
- 부모 태그에 적용시 거기 안에 있던 태그들까지 전부 상속
- 글자와 관련된 스타일들이 주로 inherit 됨

### **3. 레이아웃 만들기 1 : 호환성 좋은 float**

- <div>태그는 기본적으로 inline 속성이 있어 한 줄을 차지
- 한 줄에 여러개의 <div>태그를 넣기위해서는 float 속성을 적용
- 적용한 후에는 clear 속성을 통해 해제 필요

```CSS
.content {
  text-align: center;
}

.box {
  margin: 20px;
  padding: 30px;
  border: 1px solid black;
  border-radius: 5px;
}

.container {
  width: 800px;
}

.header {
  width: 100%;
  height: 50px;
  background-color: aquamarine;
}

.left-menu {
  float: left;
  width: 20%;
  height: 400px;
  background-color: cornflowerblue;
}

.right-menu {
  float: left;
  width: 80%;
  height: 400px;
  background-color: coral;
}

.footer {
  clear: both;
  width: 100%;
  height: 100px;
  background-color: grey;
}
```

- float 된 요소와 margin을 주기위해서는 가짜 div를 만들면 편함

```CSS
<div style="float:left"><div> /* float 된 요소 */
<div style="clear:both"></div> /* margin을 위한 가짜 div */
<div style="margin-top:10px"></div> /* margin을 주고 싶은 요소 */

```

![레이아웃 화면 예시](https://user-images.githubusercontent.com/86667412/151918896-b222c2cf-9b00-4e71-affd-2c9a872256f1.png)

### **4. 레이아웃 만들기 2 : 귀찮은 inline-block**

| 종류                 | 설명              |
| -------------------- | ----------------- |
| display:block        | 한 행을 전부 차지 |
| display:inline-block | 내 크기만큼 차지  |

- float 속성 외에 한 줄에 여러 개의 컨텐츠를 넣을 때 사용
- 단 여러개의 콘텐츠 사이에 공백을 제거해야 나란히 놓임

  - 방법 1 - 주석처리 기호 이용

    ```CSS
      <div>
        <div class="left-box"></div><!--
      --><div class="right-box"></div>
      </div>
    ```

  - 방법 2 - 부모 태그에 font-size:0px

    ```CSS
      <div style="font-size : 0px;">
          <div class="left-box"></div>
          <div class="right-box"></div>
      </div>
    ```

- inline-block 내에서 글씨 삽입 시 레이아웃이 깨지는 현상 발생(사진)
- 글자로 인해 baseline이 존재하면 inline-block 요소들이 baseline의 위로 오려고 함

### **5. 레이아웃 만들기 3 : 편리한 Flexbox**

- 부모 요소에 display:flex 속성을 주면 하위요소들이 가로로 정렬

  ```CSS
    display:flex; /* 하위 요소들에 flex 레이아웃 적용 */
    flex-direction: row /* column(기본, 가로 배치), row(세로 배치) */
    flex-wrap : wrap /* width가 큰 요소를 아래로 보내고 싶을 때 */
  ```

  - flex box의 세부속성

  ```CSS
    .flex-container {
      display : flex;
      justify-content : center;  /* 좌우정렬 */
      align-items : center;  /* 상하정렬 */
      flex-direction : column; /* 세로정렬 */
      flex-wrap : wrap;  /* 폭이 넘치는 요소 wrap 처리 */
      }
    .box {
      flex-grow : 2;  /* 폭이 상대적으로 몇배인지 결정 */
    }
  ```

### **6. flex를 이용해 반응형 웹페이지 만들기**

- PC에서는 4열, 태블릿에서는 2열, 모바일에서는 1열로 노출
- 기본적인 container에 대한 설정 후 미디어쿼리에 각각 설정

```CSS
.container {
  width: 80%;
  margin: auto;
  margin-top: 50px;
  margin-bottom: 50px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  text-align: center;
}

.list {
  width: 25%;
}

@media screen and (max-width: 1200px) {
  .list {
    width: 50%;
  }
}

@media screen and (max-width: 768px) {
  .list {
    width: 100%;
  }
}

```

### **7. div와 유사한 태그들**

- 기능은 div와 동일하나 사용처에 따라 의미를 알려주는 태그가 있음
- 상황에 따라 <nav>, <section>, <footer> 등의 태그 사용 가능

![스크린샷 2022-02-01 오후 3 21 32](https://user-images.githubusercontent.com/86667412/151921811-7a08eb0b-4bce-4502-8a4b-80873ccd63c1.png)

[참고자료 - 코딩애플 HTML/CSS 강의](https://codingapple.com/)
