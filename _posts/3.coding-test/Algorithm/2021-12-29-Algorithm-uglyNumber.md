---
title: "[Algorithm] Array-uglyNumbers"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - Array
last_modified_at:
---

## **1. uglyNumbers**

### 1. 문제

아래와 같이 정의된 ugly numbers 중 n번째 수를 리턴

- ugly number는 2, 3, 5로만 나누어 떨어지는 수
- 1은 1번째 ugly number
- 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, 16, ...

### 2. 나의 풀이

- 정의는 단순하지만 ugly number를 찾는게 어렵다는 걸 알게되었다
- ~로만 나눠진다는 개념이 생소하고, 코드로 구현한 적이 없어 어려웠다

  ```javascript
  const uglyNumbers = function (n) {
    const ch = Array.from({ length: 1000000 }, () => 0);
    const answer = [1];
    ch[1] = 1;
    let i = 1;
    let cnt = 0;
    while (answer.length < n && cnt < 1000) {
      if (ch[i / 2] === 1 || ch[i / 3] === 1 || ch[i / 5] === 1) {
        answer.push(i);
        ch[i] = 1;
      }
      i++;
      cnt++;
      console.log(answer);
    }
    return answer[n - 1];
  };
  ```

### 3. 문제 상황

- BFS/DFS방식으로 찾으려니 순서가 뒤바뀔 수 있음
- 나중에 정렬한다고 하니 n번째 uglyNumber를 찾기위해

### 4. 모범 답안 및 해설

- 2,3,5 배수별 포인터를 가지고 각 숫자별로 탐색

  ```javascript
  const arr = function (n) {
    const arr = [1];
    // ! 2, 3 ,5배수 별로 각각의 포인터를 가짐
    let idx2 = 0,
      idx3 = 0,
      idx5 = 0;

    for (let i = 0; i < n; i++) {
      // ! n의 배수별 포인터에 n을 곱하고 그중 가장 작은 값을 답에 넣음
      const a = arr[idx2] * 2;
      const b = arr[idx3] * 3;
      const c = arr[idx5] * 5;
      const next = Math.min(a, b, c);
      arr.push(next);

      // ! 답에 넣은 배수만 포인터를 증가 시킴
      // ! 12처럼 공배수의 경우에는 동시에 포인터 증가하여 배제 가능
      // ! 만약 동시에 등장하지 않더라도 최소값이 아니면 다음턴에 그대로 값이 유지되면서 언젠가 배제 됨
      if (next === a) idx2++;
      if (next === b) idx3++;
      if (next === c) idx5++;
    }
    return arr[n - 1];
  };
  ```

### 5. 깨달은 점

- 단순한 문제처럼 보여도 특정적인 해결책이 필요할 때가 있다
- 너무 한 문제에 너무 많은 시간을 투자하기 보다는 해답을 봐야할 때가 있다
