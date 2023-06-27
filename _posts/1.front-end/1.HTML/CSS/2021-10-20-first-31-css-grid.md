---
title: "[CSS] CSS 기초 - 반응형 웹 & 그리드 레이아웃"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - HTML/CSS
tags:
  - grid
last_modified_at:
---

### **1. 반응형 웹**

- 화면 크기가 다양한 모바일 기기가 등장함
- 이에 맞춰 요소를 재배치하거나 표시 방법을 바꿈.

`<code>`

### **2. 뷰포트**

1. 뷰포트의 의미

- 모바일 화면에서 실제 내용이 표시되는 영역

<small> - webkit 기반의 모바일 기본 뷰포트 너비는 '980px'</small>  
<small> - webkit: 많은 모바일 브라우저의 실행엔진</small>

1. 뷰포트 지정

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1" /* 가장
   많이 사용하는 뷰포트 속성*/ /* 너비를 모바일화면에 맞추고 초기 배율을 1로
   지정*/
   ```

2. 뷰포트 단위

   | 이름 | 의미                                         |
   | ---- | -------------------------------------------- |
   | vw   | 1vw는 뷰포트 너비의 1%                       |
   | vh   | 1vh는 뷰포트 높이의 1%                       |
   | vmin | 1vmin은 뷰포트의 너비와 높이 중 작은 값의 1% |
   | vmax | 1max은 뷰포트의 너비와 높이 중 큰 값의 1%    |

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1" /* 가장
   많이 사용하는 뷰포트 속성*/ /* 너비를 모바일화면에 맞추고 초기 배율을 1로
   지정*/
   ```

## **3. 미디어쿼리**

1. 미디어쿼리의 의미

- 기기의 해상도에 따라 다른 스타일 시트 적용
- 보통 속도나 화면크기에서 모바일의 제약이 많아 모바일의 레이아웃을 기본으로 CSS 제작(모바일퍼스트)

1. 미디어쿼리 적용

   1. 외부 CSS파일로 연결
   2. 웹 문서에 직접 정의하는 방법

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1" /* 가장
   많이 사용하는 뷰포트 속성*/ /* 너비를 모바일화면에 맞추고 초기 배율을 1로
   지정*/
   ```

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1" /* 가장
   많이 사용하는 뷰포트 속성*/ /* 너비를 모바일화면에 맞추고 초기 배율을 1로
   지정*/
   ```

## **4. 그리드 레이아웃**

- 반응형 웹에서 화면에 따라 요소를 재배치할 때 기준 필요
- 이 때 웹 사이트를 여러개의 column으로 나눈 후 배치하는 것이 '그리드 레이아웃'
- 시각적으로 안정(익숙) / 업데이트 편함 / 요소 자유배치 가능

1. 그리드 레이아웃을 만드는 방법

a. 플렉서블 박스 레이아웃

- 수평, 수직 중 한 쪽을 '주축'으로 정하고 박스 배치
- flex box layout, 보통 flex box라고 부름
- IE11에서는 부분적으로만 지원함

b. CSS 그리드 레이아웃

- '주축' 개념이 없고 수평, 수직 어느 방향이든 배치
- 대부분의 모던 브라우저에서 사용 가능

## **5. 플렉스 박스 레이아웃**

1. 기본용어  
   a. 플렉스 컨테이너 : 플렉스 박스 적용 대상을 묶음
   b. 플렉스 항목 : 플렉스 박스 레이아웃을 적용하는 대상
   c. 주축 : 플렉스 박스에서 항목을 배치하는 기본방향
   d. 교차축 : 주축과 교차하는 방향

![플렉스 박스 용어](images/../../_posts/images/2021-10-20-image.png)

2. 컨테이너 & 방향 관련 속성

   1. display 속성 - 플렉스 컨테이너 지정

   ```css
   .container {
     display: flex;
   } /*플렉스 항목을 블록 레벨 요소로 배치*/
   .container {
     display: inline-flex;
   } /*플렉스 항목을 인라인 레벨 요소로 배치*/
   ```

   <small>- display에 flex속성은 부모요소에 적용</small>  
    <small>- 자식요소는 flex라는 속성에 값 적용</small>

   2. flex-direction 속성 - 플렉스 방향 지정
      ```css
      .container {
        display: flex;
        flex-direction: row;
      } /*주축을 가로, 왼->오로 배치 (기본값)*/
      ```
   3. flex-wrap 속성 - 플렉스 줄바꿈 여부 지정
      ```css
      .container {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
      } /*너비보다 많은 플렉스 항목이 있을 때 줄안바꿈(기본)*/
      ```

3. 축 설정 관련 속성

   1. justify-content 속성 - 주축에서 항목 간 정렬 방법
      |종류|설명|
      ---|---
      flex-start|주축의 시작점에 맞춰 배치
      flex-end|주축의 끝 점에 맞춰 배치
      center|주축의 중앙에 맞춰 배치
      space-between|주축의 양 끝에 배치 후 그 사이에 배치
      space-around|모든 항목을 주축에 같은 간격으로 배치

      ```css
      .container {
        justify-content: flex-start;
      } /*항목을 주축의 시작점에 맞춰 배치*/
      ```

   2. align-items 속성 - 교차축에서 항목 간 정렬 방법
      |종류|설명|
      ---|---
      flex-start|교차축의 시작점에 맞춰 배치
      flex-end|교차축의 끝 점에 맞춰 배치
      center|교차축의 중앙에 배치
      baseline|교차축의 문자 기준선에 맞춰 배치
      stretch|플렉스 항목을 늘려 교차축에 가득 차게 배치
      ```css
      .container {
        align-items: flex-start;
      } /*항목을 교차축의 시작점에 맞춰 배치*/
      ```

4. flex 속성의 하위 속성

   1. flex의 기본속성 : grow, shrink, basis  
       `flex: <grow> <shrink> <basis>`
      ```css
      p {
        flex: 0 1 auto;
      } /* flex속성의 기본값 */
      ```
   2. grow (팽창 지수)

      - 값을 1로 설정 시 가능한 모든 영역을 차지
      - 모든 자식 박스가 동일한 0이상 값을 가지면 동일비율 차지
      - 일부 요소가 값이 크다면 비율대로 나눠 가짐\

   3. shrink (수축 지수)

      - width나 flex-basis 속성에 따른 비율이라 크기 예측 어려움
      - 둘 다 동시에 사용 보다는 shrink 을 기본값(1)로 지정

      ```css
      p {
        flex: <grow 값> 1 auto;
      }
      ```

   4. basis - 기본 크기
      - 자식박스가 grow나 shrink에 의해 변화하기 전의 크기
      - flex-grow의 속성 값이 0인 경우에만 유지 됨
      - 콘텐츠가 많아 넘치는 경우 width가 정확한 크기 보장 X
      - width와 동시 적용 시 flex-basis가 우선

5. 기타

   1. 레이아웃 리셋

      - 박스의 시작을 (0,0)으로 하고 싶을 때(기본여백 제거)
      - 페이지 구성 시 여백을 포함해 계산
      - 브라우저 마다 여백/글꼴 등 기본 스타일이 다름
      - 라이브러리 또는 아래 코드 사용

      ```css
      * {
        box-sizing: border-box;
      }

      body {
        margin: 0;
        padding: 0;
      }
      ```

   2. flex-wrap 속성

      - 콘텐츠 길이의 합이 너비를 초과할때의 처리

      ```css
      .item {
        flex-wrap: wrap;
      }
      ```

   3. order 속성

      - 기본 값은 0이고 양수/음수로 바꿔 순서롤 조정
      - 음수일 경우 양수보다는 최상단으로 이동

      ```css
      .item {
        order: 1;
      }
      ```
