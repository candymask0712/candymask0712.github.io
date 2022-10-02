---
title: "[React] 토이 프로젝트 개선기 02. 테스팅 도입"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - React-testing-library
  - RTL
last_modified_at:
---

### 1. 개요

부트캠프 중 프로젝트를 진행하면서 시간 상의 문제로 아쉬움이 남았던 부분들이 많았다.  
대부분 구현에 필수적이지는 않지만, 코드의 유지보수나 사용자 경험에 있어서는 중요한 부분들이다.  
그래서 10월 연휴를 맞이하여 그간 아쉬움이 남았던 부분들을 개선해 보려고 한다.

### 2. 개선 내용

- 테스팅 라이브러리 셋팅
- 기본 테스트 적용 시 충돌이 나는 부분 해결

### 3. 현재 상황

기존에 제작 된 프로젝트에 테스트코드를 적용하고 싶어 살펴보았다.  
CRA로 만든 프로젝트이기에 React에서 가장 많이 사용되는  
Jest와 RTL은 설치되어 있었으나 테스트 관련 파일들을 이미 지워버린 상태였다.  
이미, 코드가 다수 작성 된 상태에서 시작을 하니 본격적인 테스트 코드 작성 전에도  
여러가지 문제가 발생하였다.  

Jest와 RTL로 검색 시 많은 자료들이 새로 생성한 프로젝트에
테스트를 추가하는 방법을 설명해주고 있어 내가 겪은 케이스들을 찾기 어려웠다.  
나처럼 빠르게 제작한 프로젝트에 완성도를 높히고 싶은 사람들도 있을 것으로 생각되어
이 글에서 겪었던 문제와 해결 방법을 기록하고 공유하려고 한다.  

### 4. 개선 적용

- 먼저 테스트 도입을 위해 CRA 생성 시 만들어지는 테스트 파일을 그대로 붙여 넣었다.

```javascript
// (App.test.tsx)

import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

```javascript
// (setupTests.ts)

import '@testing-library/jest-dom';
```

```javascript
npm run test
```
코드를 적용 후 테스트를 실행하니 단순한 fail이 아닌 에러가 출력되었다

![](https://user-images.githubusercontent.com/86667412/193461320-ff827fd3-9618-4104-ae37-c64dc1b6dea5.png)

메세지의 내용은 컴포넌트가 `Provider`로 감싸져 있어야 한다는 내용이고  
검색을 해보아도 주로 같은 내용에 대한 답변이 달려 있었다.
그러나 해당 프로젝트에서는 `App` 컴포넌트를 `Provider`로 잘 감싸고 있는 구조였기에 당황스러웠다.

그러나 결국 문제는 구현 코드가 아닌 테스트코드에서 Wrapping이 되어 있어야 하는 것이었다.
그래서 index.tsx 와 동일하게 환경을 구성하기 위해, test 코드에서도 동일하게 Wrapping 해주었다.

```javascript
// (App.test.tsx)

import { render, screen } from '@testing-library/react';
import App from './App';
import { ThemeProvider } from 'styled-components';
import { theme } from './theme';

import { Provider } from 'react-redux'
import store from './redux/configStore';

test('renders learn react link', () => {
  render(<Provider store={store}><ThemeProvider theme={theme}><App /></ThemeProvider></Provider>);
  const linkElement = screen.getByText("learn react");
  expect(linkElement).toBeInTheDocument();
});
```

코드를 바꾸니 테스트는 통과하였으나 다른 문제가 발생하였다.
```
Error: Not implemented: window.scrollTo
```
![](https://user-images.githubusercontent.com/86667412/193461762-e2b51b40-6c8e-4563-bf0a-52845b2827df.png)

아래와 같이 `scrollTo` 에 대한 내용을 `setupTests.ts` 에 추가함으로써 해결하였다 

```javascript
// (setupTests.ts)

import '@testing-library/jest-dom';
const noop = () => {};
Object.defineProperty(window, 'scrollTo', { value: noop, writable: true });
```

본격적인 테스트를 시작하지는 못했지만 그래도 문제가 잘 해결되어서 좋았다.
이어서 본격적인 테스트도 시작하고 다른 부분도 개선해 나가야 겠다.