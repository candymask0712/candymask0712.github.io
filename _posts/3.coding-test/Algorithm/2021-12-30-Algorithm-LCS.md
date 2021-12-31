---
title: "[Algorithm] DP-LCS"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - LCS
  - DP
last_modified_at:
---

## **1. LCS**

### 1. 문제

두 문자열을 입력받아 다음의 조건을 만족하는 LCS\*의 길이를 리턴

- LCS: 두 문자열에 공통으로 존재하는 연속되지 않는 부분 문자열
- 문자열 'abc'의 subseqeunce는 'a', 'b', 'c', 'ab', 'ac', 'bc', 'abc'

### 2. 나의 풀이

- 풀이 실패

### 3. 문제 상황

- 문제를 정확히 이해하지 못해 풀이 실패

### 4. 모범 답안 및 해설

```javascript
const LCS = function (str1, str2) {
  const M = str1.length;
  const N = str2.length;
  const table = [];

  for (let i = 0; i < M + 1; i++) table.push(Array(N + 1).fill(-1));

  for (let i = 0; i <= M; i++) {
    for (let j = 0; j <= N; j++) {
      // ! 한 쪽 문자 길이 0 => 만들 수 있는 LCS 없음
      if (i === 0 || j === 0) table[i][j] = 0;
      // ! 두 문자 같음 => 이전 인덱스에서 만들 수 있던 LCS길이 보다 1 증가
      else if (str1[i - 1] === str2[j - 1])
        table[i][j] = 1 + table[i - 1][j - 1];
      // ! 두 문자 다름 => 한 쪽을 포기하여 만들 수 있는 LCS의 최대 길이 따름
      else table[i][j] = Math.max(table[i - 1][j], table[i][j - 1]);
    }
  }
  return table[M][N];
};
```

### 5. 깨달은 점

- 스스로 풀지 못한 문제라 모범 답안을 열심히 복습해야겠다
