---
title: "[CSS] HTML/CSS- 3 - 애니케이션 구현 "
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

### **1. one-way 애니메이션 만드는 step**

- 시작 스타일 만들기
- 최종 스타일 만들기
- 언제 최종 스타일로 변하는지 작성
- transtion으로 애니메이션 효과 적용

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
