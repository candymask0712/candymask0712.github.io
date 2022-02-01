---
title: "[CSS] HTML/CSS 강의 - 2 - 웹페이지 꾸미기 "
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

### **1. 배경 이쁘게 넣는 스킬들 & margin collapse**

- 배경을 넣을 때 유용한 옵션들

```CSS
.main-background {
  width: 100%;
  height: 500px;
  background-image: url(shoes.jpeg); /* 배경넣기 */
  background-size: cover; /* 이미지 전체가 보여지나 영역을 다 못채울 수도 */
  background-size: contain; /* 이미지가 일부 잘리더라도 영역을 다 채움 */
  background-repeat: no-repeat; /* 공간이 남을경우 반복여부 */
  background-position: center; /* 배경의 정렬 방법 */
  background-attachment: fixed; /* 마우스 스크롤에 따른 배경의 이동 여부 */
  filter: brightness(70%); /* 엣지 이상에서 사용 가능한 필터 기능 */
}

```

- margin collapse 현상 : 테두리가 겹칠 시 마진을 공유하는 현상
- 위 아래에서 겹치는 경우에도 발생 (각각 마진을 주어도 큰 것을 적용)
- 이를 해결하기 위해서는 테두리를 겹치지 않게 하거나 감안해서 코딩해야함

![스크린샷 2022-02-01 오후 5 43 15](https://user-images.githubusercontent.com/86667412/151937354-b4d0271d-1975-4352-9963-c32c9af70d03.png)

![스크린샷 2022-02-01 오후 5 45 47](https://user-images.githubusercontent.com/86667412/151937676-7ed2bb07-880b-41a5-b23e-4a05d8a0dc5c.png)

### **2. position과 좌표 레이아웃 만들기**

- 포지션 옵션 설정 후 원하는 대로 이동 가능
- 포지션 설정 시 float 처럼 공중에 뜨게 됨

```CSS
.box {
  position : static; /* 기준이 없음 (좌표적용 불가) */
  position : relative; /* 기준이 내 원래 위치 */
  position : absolute; /* 기준이 내 부모 (relative를 가진) */
  position : fixed; /* 기준이 브라우저 창 (viewport) */
}

```

- absolute 를 적용한 요소 가운데 정렬

```CSS
.button {
  position : absolute;
  left : 0;
  right : 0;
  margin-left : auto;
  margin-right : auto;
  width : 적절히
}
```

### **3. form & input**

- input의 type에 따라 적용되는 CSS 스타일링을 할수도 있음

```CSS
input[type=email] {
  color : grey
}
```

- <label> 태그와 for 속성 활용 시 label을 눌러도 input 선택됨
- 그 외에도 <input>에 제목이 필요시, <h>, <p>대신 사용

```CSS
<input type="checkbox" id="subscribe">
<label for="subscribe">누르기</label>
```

![스크린샷 2022-02-01 오후 9 05 50](https://user-images.githubusercontent.com/86667412/151965515-31b8a658-82d1-46bf-91f9-819aed47610b.png)

### **4. table**

- 먼저 <tr> 태그로 행을 만들고, 그 안에 <td>태그로 열을 넣어줌
- <td>태그 대신 <th>태그를 쓰면 제목처럼 굵게 처리 됨
- <thead>, <tbody>태그는 헤드부분 영역구분 목적으로 효과는 없음

```JS
<table>
  <thead></thead>
  <tbody>
    <tr>
      <td>내용</td>
      <td>내용</td>
    </tr>
  </tbody>
</table>
```

- 표 안에 있는 border에 틈을 없애기 위한 처리는 table에 적용

```CSS
table {
  border-collapse: collapse;
}
```

- vertical-align 속성 사용 시 테이블 셀 내와 Inline 요소 간 상하정렬 가능

![스크린샷 2022-02-01 오후 9 27 07](https://user-images.githubusercontent.com/86667412/151968143-224aae28-c344-410c-b86d-2ace8766793b.png)

### **4. pseudo-class로 인터랙티브 버튼 만들기**

- 버튼 임을 알려주기 위해 cursor 속성을 변경하면 좋음

```CSS
.btn{
  cursor:pointer
}
```

- pseudo-class 셀렉터 사용 시 상태에 따른 스타일을 지정
- 아래 3개 동시 적용시 hover -> focus -> active 순으로 적용 필요

```CSS
.btn:hover {
  background : chocolate; /*마우스를 올려놓을 때*/
}
.btn:focus {
  background : red; /*클릭 후 계속 포커스 상태일 때*/
}
.btn:active {
  background : brown; /*클릭 중일 때*/
}
```

- 기타 다양한 셀렉터

```CSS
:any-link /*방문 전, 방문 후 링크 한번에 선택할 때*/
:playing /*동영상, 음성이 재생중일 때*/
:paused /*동영상, 음성이 정지시*/
:autofill /*input의 자동채우기 스타일*/
:disabled /*disabled된 요소 스타일*/
:checked /*체크박스나 라디오버튼 체크되었을 때*/
:blank /*input이 비었을 때*/
:valid /*이메일 input 등에 이메일 형식이 맞을 경우*/
:invalid /*이메일 input 등에 이메일 형식이 맞지 않을 경우*/
:required /*필수로 입력해야할 input의 스타일*/
:nth-child(n) /*n번째 자식 선택*/
:first-child /*첫째 자식 선택*/
:last-child /*마지막 자식 선택*/
```

[참고자료 - 코딩애플 HTML/CSS 강의](https://codingapple.com/)
