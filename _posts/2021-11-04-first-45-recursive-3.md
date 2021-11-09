---
title: "[Algorithm] 이진트리(DFS) - 순열"
excerpt: "21년 11월 04일 공부일지"
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

### **1.재귀함수를 이용한 순열 만들기**  
  
#### 1. 중복 순열 구하기

```javascript
function solution (total, pick) {
    // total은 전체 대상 숫자
    // pick은 그 중에서 고를 숫자 개수를 의미
    let answer = [];
    let tmp=Array.from({length:pick},()=>0)
    // 고를 숫자의 길이만큼 배열 생성하기
    // 이후 재귀에서 동적으로 여기에 값을 담아줌
    function DFS (L){
        if(L===pick) {
        answer.push(tmp.slice())
        // 배열은 반드시 얕은복사 이상을 해주어야 함
        // 그렇지 않으면 최종 값 기준으로 기존 배열들이
        // 전부 [3, 3] 이런식으로 값이 변하게 됨
        } else {
        for(let i=1; i<=total; i++){
        // for문이 가지의 개수만큼 돌아야 함
        // i는 실제로 정답에 찍히는 숫자이므로 1부터 시작
            tmp[L]=i
            // tmp의 L번째 자리에 유동적으로 i를 할당
            DFS(L+1)
        }
        }
    }
    DFS(0)
    // 깊이의 넘버링과 정답도출은 무관하므로 0부터 시작
    return answer
}

console.log(solution(3,2))
```

1. 



```javascript
```
`<code>` 코드강조

[링크명](링크주소)    
![대체텍스트](이미지주소)

*** 
수평선

>인용
>>인용2

| | |
---|---
| | |
| | |

| | |
---|---
| 
|

<small></small>