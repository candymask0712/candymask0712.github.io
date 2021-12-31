---
title: "[Algorithm] String-ceasarCode"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Algorithm
tags:
  - String
last_modified_at:
---

## **1. ceasarCode**

### 1. 문제

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 시저암호 구현

- 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성
- 공백은 아무리 밀어도 공백
- n은 1 이상, 25이하인 자연수

### 2. 나의 풀이

- n이 음수나 25보다 큰 자연수가 입력될 수 있다 착각해 난이도에 비해 시간 지연
- 경우의 수를 쉽게 나누고 싶다는 생각에 제대로 나누지 못함

  ```javascript
  // ! 테케 3개가 모두 통과 했으나 채점은 모두 실패
  // ! 당황하고 제대로 대처 지연 => 차분한 접근 필요

  const solution = (s, n) => {
    let arr = s.split("");
    console.log(arr);
    for (let i = 0; i < arr.length; i++) {
      let tmp = s.charCodeAt(i);
      if ((tmp >= 65 && tmp <= 90) || (tmp >= 97 && tmp <= 122)) {
        if (arr[i] === arr[i].toUpperCase()) {
          // ! 대문자 + 한바퀴 더도는 경우의 수에서 더하는 숫자를 잘못설정
          // ! 태케가 여러 개라 커버가능하다고 지레짐작했음
          // ! 이 문제에서 기본적인 케이스이므로 좀 더 체계적 접근 필요
          if (tmp + n > 90) tmp = ((tmp + n) % 90) + 64;
          else tmp = tmp + n;
        } else {
          if (tmp + n > 122) tmp = ((tmp + n) % 122) + 96;
          else tmp = tmp + n;
        }
        let str = String.fromCharCode(tmp);
        arr[i] = str;
      }
    }
    return arr.join("");
  };

  console.log(solution("AB", 1)); // "BC"
  console.log(solution("z", 1)); // "a"
  console.log(solution("a B z", 4)); // "e F d"
  // ! 위 테케에서 검증하지 못하는 대문자이고 한바퀴 이상 도는 경우의 수 포함
  console.log(solution("AaZz", 25)); // "ZzYy"
  ```

### 3. 문제 상황

- 대문자/소문자, 아스키코드 범위 이내/초과의 4가지 경우의 수를 제대로 대응하지 못함

### 4. 모범 답안 및 해설

- 1

  ```javascript

  ```

### 5. 깨달은 점

- 1
