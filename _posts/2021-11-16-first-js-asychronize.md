---
title: "[javascript] 비동기 JS (Promise, async/await)  "
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - javascript
tags:
  - Promise
  - async
  - await
last_modified_at:
---

### **1. 동기와 비동기**

- 동기(Synchronous) : 입력 된 순서대로 작업을 순차적 처리
- 비동기(Asynchronous) : 이전에 입력 된 작업이 다음 작업을 block 하지 않음
- 비동기의 예시 : 타이머 API, 서버요청(fetch, AJAX 등)

### **2. callback 함수**

- 작업 중 호출을 위해 고차함수의 인자로 콜백함수가 전달
- 콜백함수는 여러번 중첩 시 복잡도가 높아진다(callback hell)

```javascript
const printStrting = (string, callback) => {
    setTimeout(
      () => {
        console.log(string)
        callback()
      },
      Math.floor(Math.random()*100) +1
    );
  }

  const printAll = () => {
    printStrting("A", () => {
      printStrting("B", () =>{
        printStrting("C", () => {})
      })
    })
  }
}
// A,B,C 순서대로 출력을 위해 콜백함수 사용
// 중첩이 생길수록 복잡도가 너무 높아짐
```

### **3. Promise 함수**

- 콜백함수 대시 비동기처리를 관리할 수 있는 함수

```javascript
const printStrting = (string) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log(string);
      resolve();
    }, Math.floor(Math.random() * 100) + 1);
  });
};

const printAll = () => {
  printStrting("A")
    .then(() => {
      return printStrting("B");
    })
    .then(() => {
      return printStrting("C");
    });
};
printAll();
// 기존 중첩된 콜백함수와 동일하게 작동
// than을 사용하여 순차적 실행되어 가독성 좋음
```

- 여러 함수를 병렬적으로 실행하는 예시

```javascript
function getUp() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("1. get up");
    }, 500);
  });
}

function typeCode() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("2. type code");
    }, 400);
  });
}

function eatDinner() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("3. eat Dinner");
    }, 300);
  });
}

function goToBed() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("4. goToBed");
    }, 200);
  });
}

getUp()
  .then((data) => {
    console.log(data);
    return typeCode();
  })
  .then((data) => {
    console.log(data);
    return eatDinner();
  })
  .then((data) => {
    console.log(data);
    return goToBed();
  })
  .then((data) => {
    console.log(data);
  });

// 다른 종류의 함수들도 직관적으로 순차실행 가능
```

### **4. Async / Await 함수**

- Promise를 좀 더 쉽게 관리할 수 있는 신문법

```javascript
function getUp() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("1. get up");
    }, 500);
  });
}

function typeCode() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("2. type code");
    }, 400);
  });
}

function eatDinner() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("3. eat Dinner");
    }, 300);
  });
}

function goToBed() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("4. goToBed");
    }, 200);
  });
}

const result = async () => {
  const one = await getUp();
  console.log(one);

  const two = await typeCode();
  console.log(two);

  const three = await eatDinner();
  console.log(three);

  const four = await goToBed();
  console.log(four);
};
// 굳이 코드를 이어서 쓰지 않아도 순차처리 가능
```
