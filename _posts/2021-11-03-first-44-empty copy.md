---
title: "[Algorithm] 이진트리(DFS) - 부분집합"
excerpt: "21년 11월 03일 공부일지"
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

### **1.**
`<code>`

### **1.재귀함수를 이용한 부분집합 만들기**

1. 숫자 N까지 모든 부분집합 만들기

```javascript
function solution (n) {
    let answer= [];
    let ch = Array.from({length:n}, ()=>0)
    // 위 배열을 함수 내에 생성해서 리셋되는 부작용
    // let ch=Array.from({length:n+1}, ()=>0);
    // 배열은 n + 1 개 생성
    // DFS(1)부터 시작이라 0번째 인덱스는 값이 변하지 않음
    function DFS (v) {
        if(v===n+1) {
        // 탐색하는 값인 v가 n을 초과하면 ch에 해당하는 부분집합 생성
            let tmp = '';
            for(let i=1; i<n+1; i++) {
                if(ch[i]===1) tmp += String(i)
                //  배열 값에 맞게 tmp (부분집합) 생성
            }
            if(tmp.length>0) answer.push(tmp);
            //  생성 된 tmp를 answer에 넣어줌
        }
        else {
            ch[v]=1 // v 레벨에 해당하는 값을 넣는다 (왼쪽)
            DFS(v+1) // v+1 레벨을 탐색한다 (왼쪽)
            ch[v]=0 // v 레벨에 해당하는 값을 넣는다 (오른쪽)
            DFS(v+1) // v+1 레벨을 탐색한다 (왼쪽)
        }
    }
    DFS(1);
    // 탐색을 시작할 값
    return answer;
}

console.log(solution(3))  
```

1. 숫자 N까지 모든 부분집합 만들기

```javascript
function solution (n) {
    let answer= [];
    let ch = Array.from({length:n}, ()=>0)
    // 위 배열을 함수 내에 생성해서 리셋되는 부작용
    // let ch=Array.from({length:n+1}, ()=>0);
    // 배열은 n + 1 개 생성
    // DFS(1)부터 시작이라 0번째 인덱스는 값이 변하지 않음
    function DFS (v) {
        if(v===n+1) {
        // 탐색하는 값인 v가 n을 초과하면 ch에 해당하는 부분집합 생성
            let tmp = '';
            for(let i=1; i<n+1; i++) {
                if(ch[i]===1) tmp += String(i)
                //  배열 값에 맞게 tmp (부분집합) 생성
            }
            if(tmp.length>0) answer.push(tmp);
            //  생성 된 tmp를 answer에 넣어줌
        }
        else {
            ch[v]=1 // v 레벨에 해당하는 값을 넣는다 (왼쪽)
            DFS(v+1) // v+1 레벨을 탐색한다 (왼쪽)
            ch[v]=0 // v 레벨에 해당하는 값을 넣는다 (오른쪽)
            DFS(v+1) // v+1 레벨을 탐색한다 (왼쪽)
        }
    }
    DFS(1);
    // 탐색을 시작할 값
    return answer;
}

console.log(solution(3))  
```

2. 서로 합이 같은 부분집합이 있는지 찾기
  (단 각 부분집합은 모든 요소를 활용해야함)

```javascript
function solution(arr) {
    let answer="NO", flag=0;
    let total=arr.reduce((a,b)=>a+b,0);
    // 간략한 식으로 합계를 표현
    let n=arr.length;
    function DFS(L, sum){
        if(flag) return;
        if(L===n) {
            if(sum===total/2) {
                answer="YES"
                flag=1;
                // 효울성을 위한 종료 flag
            }
        }
        else {
            DFS(L+1, sum+arr[L]);
            // 노드 탐색 시 합도 같이 구함
            DFS(L+1, sum);
        }
    }
    DFS(0,0);
    return answer;
}

let arr=[1,3,5,6,7,10];
console.log(solution(arr));
```
