---
title: "[Algorithm] DP-LIS"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - LIS
last_modified_at:
---

## **1. LIS**

### 1. 문제

정수를 요소로 갖는 문자열을 입력받아 다음의 조건을 만족하는 LIS\*의 길이를 리턴

- LIS: 배열의 연속되지 않는 부분 배열 중 모든 요소가 엄격하게 오름차순으로 정렬된 가장 긴 부분 배열
- 배열 [1, 2, 3]의 subseqeunce는 [1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]
- 엄격한 오름차순: 배열이 동일한 값을 가진 요소없이 오름차순으로 정렬되어 있는 경우

### 2. 나의 풀이

- 풀이 실패로 정답보고 풀이

  ```javascript
  const solution = (arr) => {
    let n = arr.length;
    let ch = Array.from({ length: n }, () => 0);
    ch[0] = 1;
    ch[1] = 1;
    for (let i = 2; i < n; i++) {
      let tmp = [];
      for (let j = 0; j < i; j++) {
        // ! 처음에 중간조건를 n으로 해서 오류
        if (arr[i] > arr[j]) tmp.push(arr[j]);
      }
      if (tmp.length > 0) ch[i] = ch[arr.indexOf(Math.max(...tmp))] + 1;
      // ! 처음에 if 조건이 없어 계속 오류
      // ! indexOf를 쓸 때는 배열이 비거나 하는등 -1 값이 나오지 않는지 고려
    }
    return Math.max(...ch);
  };
  let arr = [5, 3, 7, 8, 6, 2, 9, 4];
  console.log(solution(arr));
  ```

### 3. 문제 상황

- 문제를 정확히 이해하지 못해 답안을 이해하는데 초점을 맞춤

### 4. 모범 답안 및 해설

- 뒷 자리 기준으로 LIS 탐색

  ```javascript
  function solution(arr) {
    let answer = 0;
    let dy = Array.from({ length: arr.length }, () => 0);
    dy[0] = 1;
    for (let i = 1; i < arr.length; i++) {
      let max = 0;
      for (let j = i - 1; j >= 0; j--) {
        console.log(dy);
        if (arr[j] < arr[i] && dy[j] > max) {
          max = dy[j];
        }
      }
      dy[i] = max + 1;
      answer = Math.max(answer, dy[i]);
    }
    return answer;
  }
  ```

### 5. 깨달은 점

- 문제를 정확히 이해하지 못해 답안을 이해하는데 초점을 맞춤
