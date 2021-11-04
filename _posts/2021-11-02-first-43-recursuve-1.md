---
title: "[Algorithm] 재귀함수 기초 및 이진트리"
excerpt: "21년 11월 02일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - Algorithm
  - JS
  - TIL
last_modified_at:
---

### **1. 재귀함수**
- 재귀함수 : 자기 자신을 호출하는 함수
- 기저조건 : 메서드가 더 이상 반복되지 않는 조건
  (무한 함수 호출을 막기 위해 반드시 필요)
- for loop처럼 반복처리하고 특정상황에서 유용  

### **2. 스택프레임**
- 호출스택 : 엔진은 스택에 호출 중인 함수 기록
- 재귀함수 사용 시 기저조건 전까지 스택에 함수 쌓임
- 무한 재귀로 스택에 자리가 없으면 스택 오버플로우 발생

### **3. 기본예제로 보는 재귀함수**

1. 재귀함수를 이용한 콘솔 숫자 출력

```javascript
function recurFunc (x) {
  function inner (n) {
      // 1. 재귀함수 선언
      // 문제에 따라 조건들 설정
      if (n === 0) return;
      // 3. 중단 조건 설정
      else {
          console.log(n)
          inner(n-1)
          // 4. 함수 자기자신 호출 
        }
      }
      inner(x);
  }
recurFunc(3);
// 2. 재귀함수 호출
```

2. 이진트리 순회 기본

![참고영상 - 이진트리의 3가지 순회방법](https://www.youtube.com/watch?v=QN1rZYX6QaA)

```javascript
// 전위순회 부모 -> 왼쪽 -> 오른쪽
// 중위순회 왼쪽 -> 부모 -> 오른쪽
// 후위순회 왼쪽 -> 오른쪽 -> 부모
function solution (num) {
    answer="";
    function DFS(v) {
        if (v>5) return;
        else {
            answer += String(v);
            // 부모로 이동
            DFS(v*2);
            // 왼쪽 자식트리로 이동
            DFS(v*2+1);
            // 오른쪽 자식 트리로 이동
        }
    }
    DFS(num);
    return answer;
}
solution(1);
```