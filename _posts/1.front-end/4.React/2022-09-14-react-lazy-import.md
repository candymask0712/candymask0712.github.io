---
title: "[React] lazy-import"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - React-Query
last_modified_at:
---

## lazy-import란?

- SPA 특성상 빌드 시 하나의 js 파일로 변환 됨
- 하나의 파일에 모든 내용이 들어 있어 첫 페이지 로딩이 느려짐
- 메인페이지에서 활용하지 않는 페이지의 내용은 lazy-import 해오도록 처리 가능

### 1. 개요

부트캠프 중 프로젝트를 진행하면서 시간 상의 문제로 아쉬움이 남았던 부분들이 많았다.  
대부분 구현에 필수적이지는 않지만, 코드의 유지보수나 사용자 경험에 있어서는 중요한 부분들이다.  
그래서 10월 연휴를 맞이하여 그간 아쉬움이 남았던 부분들을 개선해 보려고 한다.

### 2. 개선 내용

- 코드스플리팅을 통한 사용자 경험 개선 (특히 메인페이지)

### 3. 현재 상황

먼저 현재 상태 체크를 위해 빌드를 해 보았다.
```javascript
yarn build
```
아래와 같이 하나의 js파일이 생성되는 것을 알 수 있다. (용량 1.8mb)
(.js.map 파일은 디버깅을 위해 생성되는 파일)  
  
[[TypeScript] js.map 파일은 무엇일까?](https://handhand.tistory.com/257)  
    
이는 랜딩 페이지 접속 시 원하는 기능과 무관하게 모든 내용을 불러와야 한다는 의미이고,  
SPA 방식의 약점인 초기 로딩 속도의 측면에서 나쁜 사용자 경험을 줄 수 있다.  

![](https://user-images.githubusercontent.com/86667412/193396458-2a569399-1858-47b8-8afa-8ea7941e6eb4.png)

cra-bundle-analyzer를 통해 번들링 된 js 파일을 확인해 보았다.  
```javascript
npm install -D cra-bundle-analyzer  // 설치
npx cra-bundle-analyzer             // 실행
```

소스 파일은 전혀 분할 되지 않고 대다수의 비중을 차지하는 모습이다(index.tsx) 
![](https://user-images.githubusercontent.com/86667412/193397150-6d9b9603-5cec-4c2a-8806-70ed8e79fb76.png)

소스 파일을 분할하기 위해 react의 공식문서를 참고해 작업을 진행하였다.  
모듈 기반의 스플리팅은 선별하기가 어렵다고하여, 공식 문서의 추천대로
페이지 기반의 스플리링을 먼저 시도해 보았다.  

[리액트 공식 문서- Code-Splitting](https://reactjs.org/docs/code-splitting.html)

대부분의 유저들이 한 번만 사용하게 되는 가입 관련 코드에 대해 먼저 적용해 보았다.  
최초에 불러오는 파일의 용량도 줄어들었고 (5.53MB -> 3.8MB)  
별도로 불러오는 파일들은 분리된 모습을 볼 수 있다. (파란색 배경)  

![](https://user-images.githubusercontent.com/86667412/193397932-b39b8ad5-e9de-41f5-ad1c-d2d091eb6680.png)

![](https://user-images.githubusercontent.com/86667412/193399360-82047952-bb3c-4ee2-bb69-434ead4ba980.png)

최종적으로 초기 화면에 필요하지 않은 페이지를 모두 분할하니 완전히 세분화 된 모습이다.  

![](https://user-images.githubusercontent.com/86667412/193399703-8d2b4c0a-09fd-4427-a61d-705d1abed481.png)

마지막으로 스플리팅 전후 로딩 시간의 차이를 확인해 보았다.  
현재 서버쪽 문제로 로컬에서 실행 된 상태라 정확한 체감 시간을 알 수는 없었으나  
번들된 JS 파일의 용량이 4분의 1이 되고, 비례하여 다운로드 시간이 줄어든 것을 확인할 수 있었다. (2.2MB -> 0.57MB)  
  

![](https://user-images.githubusercontent.com/86667412/193399953-58244e17-5357-4274-a5ff-9f961cbd54cb.png)
![](https://user-images.githubusercontent.com/86667412/193400142-d26d4be9-b7d1-4eee-a580-d4580ed09634.png)

간단한 방법으로 `code splitting` 을 적용해 보았다.  
페이지 기반의 가장 쉬운 방식이었는데도 효과가 생각보다 드라마틱해서 놀라웠다.  
앞으로 필요에 따라 모듈 기반의 코드 스플리팅도 적용해 볼 생각이다.  
  

특히, 어플리케이션 내에서 유난히 용량이 큰 모듈이 있다면  
별도로 코드 스플리팅을 적용하면 체감 성능의 차이가 클 것으로 생각된다.  