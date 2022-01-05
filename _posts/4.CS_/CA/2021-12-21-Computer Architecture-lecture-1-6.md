---
title: "[Computer Architecture] 컴퓨터 구조 - 6 - 부울대수와 논리식의 간편화"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Computer Architecture
tags:
  - Boolean Algebra
  - Karnaugh map
last_modified_at:
---

### **1. 부울대수(Boolean Algebra)**

- T/F 판별 논리 명제를 수학 전개 식으로 구현 (G.Boole)

- 부울 대수의 기본 법칙

  - 교환 법칙

    ```JavaScript
      A*B = B*A
      A+B = B+A
    ```

  - 결합 법칙

    ```JavaScript
      A*(B*C) = (A*B)*C
      (A+B)+C = A+(B+C)
    ```

  - 분배 법칙

    ```JavaScript
      A*(B+C) = A*B + A*C
    ```

  - 드모르간의 법칙

    ```JavaScript
      (A + B)' = A' + B'
      (A * B)' = A' * B'
    ```

[참고자료 - 드모르간의 법칙](https://ko.wikipedia.org/wiki/%EB%93%9C_%EB%AA%A8%EB%A5%B4%EA%B0%84%EC%9D%98_%EB%B2%95%EC%B9%99#:~:text=%EB%93%9C%20%EB%AA%A8%EB%A5%B4%EA%B0%84%EC%9D%98%20%EB%B2%95%EC%B9%99(%EC%98%81%EC%96%B4,%ED%95%9C%20%EA%B2%83%EC%9C%BC%EB%A1%9C%2C%20%EC%88%98%ED%95%99%EC%9E%90%20%EC%98%A4%EA%B1%B0%EC%8A%A4%ED%84%B0%EC%8A%A4)

### **2. 카노(Karnaugh) 맵**

- 논리 표현식을 간편하게 보여줄 수 있는 맵
- 카노 맵의 표현 방법

  - 만약 변수가 n개라면 카노맵은 2의n승 개의 민텀
  - 각 인접 민텀은 하나의 변수만이 변경되어야 한다
  - 출력이 1인 기본 곱에 해당되는 민텀은 1로, 나머지는 0으로 표시

[참고자료 - 컴퓨터 공학 전공 필수 강의 (패스트캠퍼스 - 현재는 수강불가)]
