---
title: "[React] Styled-Components로 만든 요소의 선언 위치 / ID값에 대하여"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - Styled-Components
  - Comong
  - rerender

last_modified_at:
---

### **1. Styled-Components로 만든 요소의 선언 위치 / ID값에 대하여**

Styled-Components를 이용해 프로젝트의 스타일링 작업 중 에러메세지를 만나게 되었다

![image](https://user-images.githubusercontent.com/86667412/154794972-99560c3c-5d7a-4360-af36-5bd8ffc55660.png)

```
checkDynamicCreation.js:32 The component styled.div with the id of "sc-jKTccl" has been created dynamically.
You may see this warning because you've called styled inside another component.
To resolve this only create new StyledComponents outside of any render method and function component.
```

스타일드 컴포넌트로 만든 `sc-jKTccl` 요소를 다른 컴포넌트 내에서 선언하면 안된다는 것이다

검색을 통해 관련 블로그를 보고 원인은 알았지만 에러가 발생한 요소의 위치를 몰라 잠깐 해맸는데  
[관련 블로그 글](https://letsgojieun.tistory.com/m/120)

클릭해보니 에러가 발생한 컴포넌트를 확인할 수 있어 금방 해결 하였다
![image](https://user-images.githubusercontent.com/86667412/154795074-1d67481b-b1a2-4981-a0d4-9b7da86d1bdb.png)

> 그런데 내가 사용한 이름이 아닌 `sc-jKTccl`라는 이름을 보고 문득 궁금증이 들었다

- 저런 네이밍은 어떤 프로세스를 통해 진행되는지
- 만약 다른 에러 발생 시 `sc-jKTccl` 이름을 보고 요소의 위치를 찾을 수 있는지

아래에 관련 글들을 보고 `sc-jKTccl` 라이브러리 내부에서 MurmurHash 알고리즘을 통해 생성한 id값이라는 것을 알게 되었다  
이 id값은 랜더링 시 hasing이 이루어져서 작성한 코드에서는 확인이 불가능 하다고 한다  
아쉽게도 따로 id를 이용해 따로 검색하는 기능은 없음

- 에러메세지의 발생 위치로 가거나
- 개발자 도구에서 어느정도 해당위치를 알때 디렉토리에서 찾아야 하는 듯

[스택오버플로우 글](https://stackoverflow.com/questions/59961697/random-classes-getting-displayed-when-we-use-styled-components)  
[관련 블로그 글](https://john015.netlify.app/styled-components%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%8F%99%EC%9E%91%ED%95%A0%EA%B9%8C#styled-components%EC%9D%98-%EB%82%B4%EB%B6%80-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC)

그리고 검색을 하면서 해당 에러가 성능적인 측면때문에 생긴다는 것을 알게 되었다
styled components를 다른 컴포넌트 내부에서 정의하면 랜더링 속도가 크게 느려질 수 있다는 것이다

[styled-components 공식 홈페이지](https://styled-components.com/docs/basics#coming-from-css)

프로젝트 진행이 바빠 괜히 찾아본다는 생각도 했었는데, 궁금증이 풀리니 기분도 좋고, 생각 외로 알게 된 내용도 많아 좋았다
사용하는 기술에 대해서는 시간나는 대로 공식홈페이지를 통해, 작동원리에 대해서도 어느정도 파악할 수 있게 노력해야 겠다.
