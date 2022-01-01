---
title: "[Algorithm] heap-binaryHeap"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - heap
last_modified_at:
---

## **1. binaryHeap**

### 1. 문제

정수를 요소로 갖는 배열을 입력받아 이진 힙(binary heap)\*을 리턴

- 이진 힙(binary heap)은 노드의 값이 특정한 순서를 가지고 있는 완전 이진 트리(Complete Binary Tree)
- 완전 이진 트리는 이진 트리의 (마지막 레벨 또는 마지막 깊이를 제외하고) 모든 레벨이 노드로 가득 채워져 있어야 함.
- 마지막 레벨은 왼쪽부터 차례대로 채워져 있음

### 2. 나의 풀이

- 없음

### 3. 문제 상황

- heap 개념이 생소하여 유튜브 영상자료를 참고하여 학습

### 4. 모범 답안 및 해설

```javascript
// ! 두 노드의 자리 교체
function swap(idx1, idx2, arr) {
  [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
}

// ! 부모 노드의 인덱스
function getParentIdx(idx) {
  return Math.floor((idx - 1) / 2);
}

// ! 힙 내에 알맞은 자리에 노드 추가
function insert(heap, item) {
  // ! 일단 힙의 가장 끝자리 노드에 값 추가
  heap.push(item);

  // ! 현재 노드의 인덱스와 부모 노드의 인덱스를 저장
  let curIdx = heap.length - 1;
  let pIdx = getParentIdx(curIdx);

  // ! 힙정렬이 되어 있는 지 비교
  // ! 최대 루트 노드까지 계산 (부모 노드의 인덱스가 0 이상) & 현재 요소가 부모 요소보다 클 때까지 계산
  while (pIdx >= 0 && heap[curIdx] > heap[pIdx]) {
    // ! 부모 노드, 현재 노드의 자리를 바꿈
    swap(curIdx, pIdx, heap);
    // ! 기존 부모 노드를 현재 노드 자리에 넣고
    curIdx = pIdx;
    // ! 현재 노드에 대해 새로운 부모 노드를 구함
    pIdx = getParentIdx(curIdx);
  }
  return heap;
}

// ! 배열을 받으면 최대힙으로 정렬
const binaryHeap = function (arr) {
  return arr.reduce((heap, item) => {
    // console.log('@@@heap','item',item,'heap',heap)
    return insert(heap, item);
  }, []);
};
```

### 5. 깨달은 점

- 노드 추가 시 다른 노드들의 자리를 바꾸는 부분이 잘 이해가 안되었었는데 이제는 많이 익숙해진 것 같다
