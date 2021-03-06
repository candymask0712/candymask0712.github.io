---
title: "[CSS] CSS 기초 - 글꼴"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - HTML/CSS
tags:
  - font
last_modified_at:
---

### **1. 글꼴 관련 스타일**

1. font-family - 글꼴
   : 사용자 시스템의 지정 글꼴이 없을 것 대비 여러 개 지정 (fallback)
   `font-family:<글꼴 이름> | [<글꼴이름2>,<글꼴이름3>]`

```javascript
body{font-family :"맑은 고딕", 돋움, 굴림}
// 두 단어 이상으로 된 글꼴은 ""로 묶어 표시
```

2. font-size - 글자크기  
   `font-size:<절대 크기>|<상대크기>|<크기>|<백분율>`  
   a. 키워드 이용 (small, medium, large 등)  
   b. 단위 이용

| 종류 | 설명                                         | 비고 |
| :--- | -------------------------------------------- | ---- |
| em   | 부모요소에서 지정한 글꼴 대문자M의 너비 기준 | 상대 |
| rem  | 문서의 시작 부분(root)에서 지정한 크기 기준  | 상대 |
| ex   | 부모요소에서 지정한 글꼴 소문자x의 높이 기준 | 상대 |
| px   | 모니터의 1px를 기준으로 한 후 비율값 지정    | 절대 |
| pt   | 포인트라고 하며 일반 문서에서 많이 사용      | 절대 |

c. 백분율 이용 (부모요소의 글꼴 크기가 단위 지정 시)

### **2. 상황별 font-size**

1. 기기 등 환경의 영향 X (인쇄) - px
2. 일반적인 경우 - rem  
   : root의 영향만 받아 em 보다 안정적 관리 가능
3. 반응형 웹에서 기준 점을 만들 때  
   : px를 기준으로 디바이스 크기별 css 적용
4. 화면 너비/높이에 따른 상대적 크기가 중요할 때  
   : vw, vh 사용 [예시사이트](https://www.krause.studio/#one])

- 다양한 단위에 대한 추가 참고자료  
  [CSS의 7가지 단위 - rem, vh, vw, vmin, vmax, ex, ch
  ](https://webclub.tistory.com/356)  
  [반응형 웹 뚝딱 만들기 (2) - vw, vh, vmin, vmax, em, rem 속성](https://nykim.work/85)

### **2. font관련 스타일링**

1. font 꾸미기

- 굵기 : font-weight
- 밑줄, 가로줄 : text-decoration
- 자간 : letter-spacing
- 행간 : line-height

2. font 정렬

- text-align
