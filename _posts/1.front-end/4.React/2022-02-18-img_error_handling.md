---
title: "[React] 배포시 아이콘이 로드되지 않는 현상 해결(feat. React의 이미지 경로)"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - icon
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
<NavNotification src="/icons/mobilenav/bell.png" />

// 에러난 이미지 코드 (하단 네비게이션 아이콘)
<NavMenuImg
  src={`/icons/mobileNav/${cartColor ? "cart-hover.png" : "cart.png"} `}
/>
```

이미지 파일이 위치한 디렉토리의 경로가 `mobileNav` 와 `mobilenav`로 달랐다  
`mobilenav`가 맞는 경로로 원래 `mobileNav` 작명하고 변경했는데 반영이 안된 것이다  
경로가 틀렸지만 로컬환경에서는 맞는 주소를 찾아 보여준 것이다

오류에 관해 검색을 하면서 리액트에서 이미지 경로를 설정하는 방법과  
빌드 방식에 대한 자료를 찾을 수 있었다

[react - 이미지 경로](https://velog.io/@hover16/react-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C-k4x2xhji)  
[리액트에서 이미지 경로 설정하기 (public, src 디렉토리 차이)](https://bokjiho.medium.com/react-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-public-src-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC-%EC%B0%A8%EC%9D%B4-fddb4f455c2a)

- public 디렉토리에 넣은 파일은 webpack으로 처리되지 않고, 원본이 build 폴더에 복사된다
- 그래서 파일이 후처리(post-process) 되거나 경량화(minify)되지 않음
- 파일 경로를 잘못 입력하거나, 해당 파일이 존재하지 않을 경우 컴파일 단계에서 오류가 발생하지 않고, 사용자가 접근할 때 404 오류를 응답받게 됨

public 디렉토리에 넣었기에 webpack으로 처리되지 않아 정확한 파일경로가 필요했던 것으로 보인다  
또한, 에러와도 별개로 경로에 따라서 후처리나 경량화 여부가 달라진다는 것을 알게 되었다

위에 적은 특성 외에도 링크에는 더욱 상세한 내용이 나와있었다  
이전까지는 별 생각없이 public폴더에서 이미지를 관리 했었는데  
이제부터는 용도에 따라 구분지어 사용해야 겠다
