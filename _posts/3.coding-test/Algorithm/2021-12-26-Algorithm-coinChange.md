---
title: "[Algorithm] DP-coinChange "
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:

last_modified_at:
---

## **1. coinChange**

### 1. 문제

다양한 동전들을 가지고 특정 금액을 만들 수 있는 모든 경우의 수를 리턴해야 합니다.

- 예를 들어, 100원, 500원짜리 동전을 가지고 1,000원을 만들 수 있는 방법은 총 3가지 입니다.
- 100원 10개, 100원 5개 + 500원 1개, 500원 2개

### 2. 나의 풀이

- 이 중 루프를 사용하여 DP 방식으로 경우의 수 계산 시도
- 과거 거스름돈 관련 유사문항과 비슷하게 풀이 시도하였으나 실패

  ```javascript
  const coinChange = function (total, coins) {
    let n = coins.length;
    let ch = Array.from({ length: total + 1 }, () => 0);
    for (let i = 0; i < coins.length; i++) {
      for (let j = coins[i]; j < ch.length; j += coins[i]) {
        ch[j] = ch[coins[i] - j] + 1;
      }
    }
  };
  ```

### 3. 문제 상황

- 일반식 작성 시 한 단위의 돈에서 낼 수 있는 경우의 수와 다음 단위에서 낼 수 있는 경우의 수를 동시에 만족하기 어려움

### 4. 모범 답안 및 해설

- 돈의 단위별로 하나의 배열을 가지는 이차원 배열을 통해 경우의 수를 정확히 나눔
- 다른 동전으로 지불가능한 경우 / 다음 동전으로 지불가능한 경우를 나누어 계산하여 문제를 해결

  ```javascript
  const coinChange = function (total, coins) {
    // ! table[i][j]는 coins[j]까지 사용 시 i만큼의 금액 만드는 경우의 수
    const table = [];
    for (let i = 0; i < total + 1; i++) table.push(Array(coins.length).fill(0));

    // ! 금액 0에 대해서는 모두 1가지의 경우의 수(지불X)
    for (let i = 0; i < coins.length; i++) table[0][i] = 1;

    // ! 금액(m)에 대해 동전의 종류(i)을 추가하며 지불 가능한 경우의 수 구함
    for (let m = 1; m <= total; m++) {
      for (let i = 0; i < coins.length; i++) {
        // ! inc : 동전 coins[i]로 지불할 수 있는 경우의 수
        // table[m - coins[i]][i]의 값이 있다면 가져옴 (같은 동전 내 이므로 행이 바뀜)
        // 2원 동전 기준 2원 지불 시 table[2][1]의 값이 1이므로 지불 가능
        let inc = 0;
        if (m - coins[i] >= 0) inc = table[m - coins[i]][i];

        // ! exc : 동전 coins[i]를 사용하기 직전까지의 지불 가능한 경우의 수
        // 2원 동전 기준 2원 지불 시 table[2][0]의 값이 1이므로 지불 가능
        // 0번째 동전은 이전 동전이 없으므로 배제
        let exc = 0;
        if (i >= 1) exc = table[m][i - 1];

        // ! 새로운 동전을 포함시 경우의 수 + 제외 시 경우의 수 합산
        table[m][i] = inc + exc;
      }
    }
    return table[total][coins.length - 1];
  };
  ```

### 5. 깨달은 점

- 기존에는 주로 일차원 배열을 사용한 DP문제를 보아 이차원으로는 구현할 생각을 못함
- 너무 기존 유형을 의식하기 보다는 필요한 내용을 세분화하고 이에 맞는 코드 작성 필요
