---
title: "[Algorithm] Queue의 기초와 기본예제"
excerpt: "21년 11월 10일 공부일지"
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - JS
tags:
  - Algorithm
  - Queue
  - Stack
  - JS
  - TIL
last_modified_at:
---

스택에 이어서 큐에 대해서 학습하였다.  
큐는 양방향으로 데이터가 이동할 수 있어 실제적인 쓰임새가 더 많을 것 같다.  
이번에 기본 개념을 확실하게 다질 수 있도록 해야겠다.  

### **1. Queue의 기초**

- Queue는 `줄 서서 기다리다`, `대기행렬` 라는 의미의 영어단어
- 한 쪽으로 들어간 데이터가 다른 방향으로 나오는 자료구조
- 먼저 들어간 데이터가 먼저 나옴(FIFO, LILO)

1. Queue의 사용 예제

- 양방향의 Queue를 활용 프린터의 buffer 구현
- buffer를 통해 컴퓨터 장치간 속도/시간차이 극복
- 장치에서 발생하는 불규칙이벤트
- FIFO 방식이므로 명령순서대로 프린터에서 인쇄 됨
- 컴퓨터 -> 버퍼(Queue) -> 프린터
  
- 프린터의 buffer를 코드로 구현한 예시
  
```javascript
function queuePrinter(bufferSize, capacities, documents) {
  const b = bufferSize;
  const c = capacities;
  const d = documents;
  let arr = Array.from({length:b},()=>0);    
  let count = 0;
  let sum = 0;

  do {
        arr.push(0);
        arr.shift();
        sum = arr.reduce((a,b)=>(a+b),0);
      if(arr[b-1] === 0 && sum + d[0] <= c){
        arr[b-1]=d[0];
        d.shift()
        count++
    } else {
        count++
    }
    sum = arr.reduce((a,b)=>(a+b),0);
  } while(sum>0 || d.length>0)
  return count
}
```
