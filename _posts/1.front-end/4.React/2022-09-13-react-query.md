---
title: "[React] react-query의 기본 코드 및 특징"
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

## React-Query란?

여러 개발 블로그에서 ajax 요청 시 유용하다고 평가하는 React-Query를 간단히 사용해 보았다.
캐싱, 데이터 패칭 등 실제로 직접 구현 시에는 부담스러운 부분들을 잘 관리해준다는 느낌이 들었다. 

### 1. react-query 설치 & 셋팅

- `npm install @tanstack/react-query`로 설치
- 아래와 같이 index.js에서 코드 작성 후 감싸줌  
  ```javascript
  // index.js 파일
  import { QueryClient, QueryClientProvider, useQuery } from '@tanstack/react-query'
  const queryClient = new QueryClient()

  const root = ReactDOM.createRoot(document.getElementById('root'));
  root.render(
    <QueryClientProvider client={queryClient}>  //3번
          <App />
    </QueryClientProvider>
  ); 
  ```

  - ajax 요청 시 useQuery로 감싸줌
    ```javascript
    function App(){
      let result = useQuery(['작명'], ()=>
        axios.get('https://codingapple1.github.io/userdata.json')
        .then((a)=>{ return a.data })
      )
    }
    ```


### 장점1. ajax 상태에 따른 코드 작성 용이

- ajax 요청 성공/실패/로딩중 상태를 쉽게 파악 및 활용 가능
    ```javascript
    function App(){
      // result 변수에 ajax 현재 상태 저장 됨
      let result = useQuery('작명', ()=>
        axios.get('https://codingapple1.github.io/userdata.json')
        .then((a)=>{ return a.data })
      )
      // ajax 상태에 따른 분기 처리 가능
      return (
        <div>
          // ajax요청이 로딩 중 => result.isLoading 이 true
          { result.isLoading && '로딩중' }
          // ajax요청이 실패 => result.error 가 true
          { result.error && '에러남' }
          //ajax요청이 성공 => result.data에 데이터 들어옴
          { result.data && result.data.name }
        </div>
      )
    }
    ```



### 장점2. ajax 요청 실패 또는 필요한 순간 자동 재요청

- 페이지 체류 후 일정 시간 경과 or 페이지 이동 등
- ajax 요청이 필요한 경우에 자동으로 ajax 요청 => 최신 데이터 보여주기에 용이
  ```javascript
  const Todos = () => {
    const { isLoading, isError, data, error } = useQuery("todos", fetchTodoList, {
      refetchOnWindowFocus: false, // 재실행 여부 옵션(사용자가 다른 윈도우 본 뒤)
      retry: 0, // 실패시 재호출 횟수
      onSuccess: data => {
        // 성공시 호출
        console.log(data);
      },
      onError: e => {
        // 실패시 호출 (401, 404 같은 error가 아니라 정말 api 호출이 실패한 경우만)
        // 강제로 에러 발생시키려면 api단에서 throw Error 날림
        console.log(e.message);
      }
    });

    if (isLoading) return <span>Loading...</span>;

    if (isError) return <span>Error: {error.message}</span>;

    return (
      // (...)
    );
  };
  ```

### 장점3. ajax 요청 결과는 prop 요청 불필요 (캐싱)

- useQuery 사용 시 지정하는 unique key가 같을 경우 자동 캐싱
- 같은 API 요청에 대해 2개 이상 존재 시 한 개만 날려줌
- 이전에 동일한 ajax 요청했다면 캐싱한 데이터를 보여줌 

 
### 고려할 점. react-query의 대체제
 
- react-query의 장점은 DB와의 실시간의 동기화
- 그러나 ajax 요청을 몇 초마다 반복하는 방식은 비효율성 존재
- 실시간 동기화에는 web socket 또는 Server-sent event 등 대안 존재
 
`react-query는 실질적으로 ajax 관련 개발에 편리한 도구`


Reference
[기억보다 기록을](https://kyounghwan01.github.io/blog/React/react-query/basic/#usequery)
[코딩애플 리액트 인터넷 강의](https://codingapple.com/)