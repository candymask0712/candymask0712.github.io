---
title: "[Algorithm] 이진트리(DFS) - 부분집합, 합계"
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
### **1.재귀함수를 이용한 부분집합 만들기**  

#### 1. 숫자 N까지 모든 부분집합 만들기

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

2. 합이 같은 부분집합 찾기

```javascript
function solution(arr) {
    let answer="NO", flag=0;
    let total=arr.reduce((a,b)=>a+b,0);
    let n=arr.length;
    function DFS(L, sum){
        if(flag) return;
        if(L===n) {
            if(sum===total/2) {
                answer="YES"
                flag=1;
// flag 사용 시 -> 스택에 남은 함수만 호출 
// 다른 재귀 호출은 없이 끝남

// flag 없이 바로 return 시 -> 호출 된 함수만 종료 
// 스택에 남은 함수는 다시 팝되어 재귀를 호출
            }
        }
        else {
            DFS(L+1, sum+arr[L]);
            DFS(L+1, sum);
        }
    }
    DFS(0,0);
    return answer;
}

let arr=[1,3,5,6,7,10];
console.log(solution(arr));
```

3. 제한 조건 내 최대합 구하기 문제
- 이전 문제와 달리 가지가 모두 뻗을 필요 없음
- 이미 합계가 제한을 초과한 가지는 return으로 가지치기

```javascript
function solution(c, arr){
    let answer=Number.MIN_SAFE_INTEGER;
    let n=arr.length;
    function DFS(L, sum){
        if(sum>c) return;
        // return 이후에 더 근접한 값이 나올 가능성?
        // 허용값을 초과하면 리턴하는데 리턴하기 않고 
        // 그대로 두면 계속 무게를 더하니 더 큰값으로 증가하겠죠.
        // return 시 전체탐색이 중단되는것이 아닌 해당 가지가 더 깊은 depth로 가는 것을 막음
        // 이 문제는 depth가 유동적일 수 있어서 가지치기가 필요
        if(L===n){
            answer=Math.max(answer, sum);
        }
        else{
            DFS(L+1, sum+arr[L]);
            DFS(L+1, sum);
        }                  
    }
    DFS(0, 0);
    return answer;
}

let arr=[81, 58, 42, 33, 61];
console.log(solution(259, arr));
```
