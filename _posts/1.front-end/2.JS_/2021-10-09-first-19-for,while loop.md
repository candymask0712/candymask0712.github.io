---
title: "[JavaScript] for, while loop의 이해"
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JavaScript
tags:
  - for loop
  - while loop
last_modified_at:
---
### 1. **for 반복문에서 조건설정을 효율적으로 하자**

for 반복문 작성 시 조건 부분을 기계적으로 작성하는 경우가 있다  
특히 i++ 은 대부분 고정이라 더욱 그렇다  
많이 반복하면 구동은 되겠지만 낭비하는 부분이 없도록 신경쓰자

- 3의 배수로 된 문자열 구하기(나의 코드)

```javascript
function makeMultiplesOfDigit(num) {
  let answer = "";
  for (let i = 1; i <= num; i++) {
    if (i % 3 === 0) answer += String(i);
  }
  return answer;
}
```

- 3의 배수로 된 문자열 구하기(좋은 코드)  
  조건 설정을 통해 최적화 함

```javascript
function makeMultiplesOfDigit(num) {
  let result = "";

  for (let i = 3; i <= num; i += 3) {
    // 첫번째 조건과 세번째 조건을 효율적으로 설정
    result = result + String(i);
  }

  return result;
}
```

### 2. **while과 do while의 차이**

while은 기본 반복문인데 자주 안써서 헷갈리는 경우가 있다  
반복 횟수가 가변적일 때 꼭 기억해야 하므로 숙지하자

#### 1) while

- 지정된 식이 false가 될 때까지 문 블록을 반복 실행
- 선 평가 후 실행문 (한번도 실행되지 않을 수도 있음)

#### 2) do while

- 지정된 식이 false가 될 때까지 문 블록을 반복 실행
- 선 실행 후 평가문 (무조건 한 번은 실행 됨)
