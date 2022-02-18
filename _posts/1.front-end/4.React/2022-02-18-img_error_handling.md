---
title: "[React] 배포 시 아이콘이 로드되지 않은 현상 해결"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - directory
last_modified_at:
---

### **1. 배포 시의 아이콘 로드 에러**

오늘 4주 프로젝트를 시작하고 클라이언트의 첫 배포가 있었다
그런데 배포를 하니 로컬에서 발생하지 않았던 이미지 오류가 있었다

![image](https://user-images.githubusercontent.com/86667412/154602254-fef90ca5-ce0e-4bc5-8de7-019b313b4af0.png)

하단 네비게이션 바를 보면 메뉴마다 아이콘이 있어야 하는데
모든 아이콘이 로드되지 않는 모습이다

나와 팀원들의 로컬환경에서는 아이콘이 잘 보이고 있어 약간 당황하였지만
상단에 있는 종 모양의 알림 아이콘은 잘 로드 되는 것을 보고 코드를 비교해 보았다

```javascript
// 정상 출력 되는 이미지 코드 (상단 알림 아이콘)

// 에러난 이미지 코드 (하단 네비게이션 아이콘)
<NavMenuImg
  src={`/icons/mobileNav/${cartColor ? "cart-hover.png" : "cart.png"} `}
/>
```

[react - 이미지 경로](https://velog.io/@hover16/react-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C-k4x2xhji)
[리액트에서 이미지 경로 설정하기 (public, src 디렉토리 차이)](https://bokjiho.medium.com/react-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-public-src-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC-%EC%B0%A8%EC%9D%B4-fddb4f455c2a)

- 내용

```javascript

```

- 내용

```javascript

```

### **1. 소제목**

1. 넘버링

- 내용

```javascript

```

- 내용

```javascript

```

```javascript

```

`<code>` 코드강조

[링크명](링크주소)  
![대체텍스트](이미지주소)

---

수평선

> 인용
>
> > 인용2

|     |     |
| --- | --- |
|     |     |
|     |     |

|     |     |
| --- | --- |
|     |     |
|     |     |
|     |     |
|     |     |
