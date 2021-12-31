---
title: "[Algorithm] DC-closestPairOfPoints"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - Divide and Conquer

last_modified_at:
---

## **1. closestPairOfPoints**

### 1. 문제

좌표평면 상의 다양한 점들을 입력받아 가장 가까운 두 점 사이의 거리를 리턴해야 합니다.

- points는 y좌표나 x좌표 등으로 정렬되어 있지 않습니다.
- 함수 calculateDistance는 소수점 계산을 피하기 위해 두 점 사이의 거리에 100을 곱한 후 반올림하여 정수 부분만 취함

### 2. 나의 풀이

- 효율성을 고려하지 않고, 모든 두 점 사이의 거리를 계산

  ```javascript
  function calculateDistance(p1, p2) {
    const yDiff = p2[0] - p1[0];
    const xDiff = p2[1] - p1[1];
    return Math.sqrt(Math.pow(yDiff, 2) + Math.pow(xDiff, 2));
  }

  const closestPairOfPoints = function (points) {
    if (points.length >= 100) return 0;
    let answer = [];
    let arr = points;
    for (let i = 0; i < arr.length; i++) {
      for (let j = 1; j < arr.length; j++) {
        let tmp = calculateDistance(arr[i], arr[j]);
        if (tmp !== 0) answer.push(tmp);
        console.log("tmp", tmp, "answer", answer);
      }
    }
    return Math.round(Math.min(...answer) * 100);
  };
  ```

### 3. 문제 상황

- 전체를 탐색하지 않고 최단거리의 점을 구할 방법이 떠오르지 않음

### 4. 모범 답안 및 해설

- 1

```javascript
// https://bblackscene21.tistory.com/11 해설 링크
function calculateDistance(p1, p2) {
  const yDiffSquared = Math.pow(p2[0] - p1[0], 2);
  const xDiffSquared = Math.pow(p2[1] - p1[1], 2);
  const dist = Math.sqrt(yDiffSquared + xDiffSquared);

  return Math.round(dist * 100);
}

// ! 3개 이하인 점에 대해 최단거리 계산
const closestPairOfPoints = function (points) {
  const bruteForce = (start, end, sorted) => {
    let min = Number.MAX_SAFE_INTEGER;

    for (let src = start; src <= end; src++) {
      for (let dst = src + 1; dst <= end; dst++) {
        const dist = calculateDistance(sorted[src], sorted[dst]);
        min = Math.min(min, dist);
      }
    }

    return min;
  };
  // ! 중간 지점에 대해 기존에 구한 최소값만큼 가까운 점이 있는지 확인
  const closestCrossing = (mid, sorted, min) => {
    // ! 중간 지점에 대해 탐색할 왼/오 포인터 지정
    const midX = sorted[mid][1];
    let lIdx = mid - 1;
    let rIdx = mid + 1;

    // ! 기존에 구한 최소값 만큼 양 옆으로 탐색할 범위 지정
    while (rIdx < sorted.length && Math.abs(midX - sorted[rIdx][1]) * 100 < min)
      rIdx++;
    while (lIdx >= 0 && Math.abs(midX - sorted[lIdx][1]) * 100 < min) lIdx--;

    for (let i = lIdx + 1; i < rIdx; i++) {
      for (let j = i + 1; j < rIdx; j++) {
        min = Math.min(min, calculateDistance(sorted[i], sorted[j]));
      }
    }
    return min;
  };

  // ! 가장 가까운 점 계산 메서드
  const closestFrom = (start, end, size, sorted) => {
    // ! DC방식으로 나누면서 점이 3개 이하가 되면 직접 계산
    if (size <= 3) return bruteForce(start, end, sorted);

    // ! 중간 지점을 구하고
    const mid = Math.floor((start + end) / 2);
    // ! 왼/오에 대해 가장 가까운 두 점을 구함
    const minLeft = closestFrom(start, mid, mid - start + 1, sorted);
    const minRight = closestFrom(mid + 1, end, end - mid, sorted);

    // ! 전체에서 가장 가까운 점을 구함
    let min = Math.min(minLeft, minRight);
    // ! 반으로 나누면서 생긴 중간 지대에도 가까운 점이 있는지 확인
    return closestCrossing(mid, sorted, min);
  };

  // ! x좌표를 기준으로 정렬
  points.sort((a, b) => a[1] - b[1]);
  // ! 전체 배열에 대해 가장 가까운 점 계산 시작
  return closestFrom(0, points.length - 1, points.length, points);
};
```

### 5. 깨달은 점

- 이번 풀이는 스스로 떠올리기는 어려운 내용이기 때문에 복습을 통해 내 것으로 만들도록 해야겠다
