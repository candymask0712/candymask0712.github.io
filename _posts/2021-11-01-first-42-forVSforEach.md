---
title: "[Algorithm] for문과 forEach의 차이  "
excerpt: "21년 11월 01일 공부일지"
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

최근 고차함수 연습을 하기위해 기존에 for를 사용해서 풀던 문제를 forEach로 바꿔보았다. 그런데 for문과는 몇 가지 차이점이 있어 여기에 정리해 놓으려고 한다

### **1.loop 반복 중 배열 변경 시의 차이점**

- 조건에 따라 문자열에 '-'를 삽입하는 문제
- loop 반복 중 대상이 변한다면 for 사용 필요

- forEach 사용 시

```javascript
// loop 중간 '-'들이 추가되면서 arr배열의 길이 변동
// 하지만 forEach는 원 배열 길이만큼만 반복
function solution(str) {
    let arr = str.split('');
    let count = 0;
    let answer=[...arr] 
    arr.forEach((el,i) =>{
        if (Number(el)%2===1 && Number(arr[i+1])%2===1) {
        answer.splice(i+1+count, 0, '-');
        count += 1;
        }
    })
    return String(answer.join(''));
}
console.log(solution('133556779294'))
// 1-3-3-5-567-7-9294

// count += 1이 없을 시
console.log(solution('133556779294'))
// 1----33--556779294
// 원래 arr의 길이를 기준으로 '-'이 삽입
```

- for 사용 시
  
```javascript
// for 문은 조건식이 거짓일 때 까지 반복문 시행
// 매 시행마다 조건식을 평가
// 따라서 증가하는 arr의 길이에 맞춰 진행 가능
function solution(str) {
    if (str === '') return false;
    let arr = str.split('');
    for (let i = 1; i<arr.length; i++) {
        // i를 1로 설정했기에 arr.length-1로 하면 끝까지 체크 불가
        if(arr[i-1]%2===1 && arr[i]%2===1) arr.splice(i,0,'-');
        // str을 arr의 요소로 전환한 것이여서 엄밀히는 Number 통해 숫자로 변환해야 함
    } 
    return arr.join('');
}
console.log(solution('133556779294'))
// 1-3-3-5-567-7-9294
```

### **2. return 등 loop 중단 시의 차이점**
- 답을 찾는 즉시 종료 가능한 문제라면 for 사용 필요

- forEach 사용 시
  
```javascript
// return 사용이 불가해 모든 요소 탐색 필수
function solution(str) {
    const arr = str.toLowerCase().split('');
    let answer = false;
    arr.forEach((el,i) => {
        if(el==='a' && arr[i+4]==='b') answer = true
        else if(el==='b' && arr[i+4]==='a') answer = true;
    })
    return answer;
}
```

- for 사용 시

```javascript
// 답을 찾는 즉시 return으로 탈출 가능
function solution(str) {
    if (str === '') return false;
    str = str.toLowerCase();
    let arr = str.split('');
    for (let i = 0; i<arr.length-4; i++) {
        if(arr[i]==='a' && arr[i+4]==='b') return true;
        else if(arr[i]==='b' && arr[i+4]==='a') return true;

    } 
    return false;
}
```

- 모범답안
  
```javascript
// 답을 찾는 즉시 return으로 탈출 가능
function ABCheck(str) {
    if (str === undefined) {
        return false;
    }

    str = str.toLowerCase();

    for (let i = 4; i < str.length; i++) {
        if (
        (str[i] === 'a' && str[i - 4] === 'b') ||
        (str[i] === 'b' && str[i - 4] === 'a')
        ) {
        // if 소괄호 내에 다시 소괄호 및 or 연산자 사용
        // 더 간단하고 사람입장에서 가독성도 좋은 코드
        return true;
        }
    }

    return false;
}
```
