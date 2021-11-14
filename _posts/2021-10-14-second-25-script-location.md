---
title: "[HTML] HTML에서 script는 어디에 위치해야 할까?"
excerpt: "위치별 장단점 및 async/defer"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - HTML
tags:
  - JavaScript
last_modified_at:
---
### **1. 객체 값으로 null이 들어가는 경우 방지**

script태그 에서 dom조작이 있을 경우 가장 하단에 위치해야 존재하지 않는 dom에 접근하는 상황을 막을 수 있다

### **2. 사용자 기준 화면 렌더링 시간 감소**

script태그를 불러오는 동안에는 html 파싱이 멈추기 때문에 사용자가 빈화면을 보는 시간을 줄일 수 있다

### **3. 그래도 script 실행이 꼭 필요하다면?**

async 또는 defer를 활용해서 해결(참고자료)

참고자료

[html파싱을 기준으로 설명한 script 태그의 위치](https://jae04099.tistory.com/entry/HTML-script-%ED%83%9C%EA%B7%B8%EB%8A%94-%EC%96%B4%EB%94%94%EC%97%90-%EC%9C%84%EC%B9%98-%ED%95%B4%EC%95%BC-%ED%95%A0%EA%B9%8C)