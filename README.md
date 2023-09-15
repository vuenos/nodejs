# Nodejs

<img src="./Node.js_logo.svg" width="240" />

> Node.js 는 Chrome V8 Javascript 엔진으로 빌드된 자바스크립트 런타임

- Node 는 V8 엔진과 더불어 libuv 라는 라이브러리를 같이 사용함. 각각 C, C++ 로 구현됨.
- libuv 는 노드의 특성인 이벤트 기반(Event-driven), 논블로킹(비동기) I/O 모델을 구현함.

## 이벤트 기반(Event-driven)
- 이벤트 기반이란 이벤트가 발생할 때 미리 지정해둔 작업을 수행하는 방식(이벤트 : 클릭이벤트, 네트트워크 요청 등)
- 특정 이벤트가 발생할 때 무엇을 할지 미리 등록해 둔다. 이를 이벤트 리스너(addEventListener)에 콜백(callback) 함수를 등록한다고 표현.
- 시스템에서 이벤트발생(클릭, 요청 등) -> 이벤트리스너(콜백 함수 등록) -> 등록된 콜백 함수 호출 -> 시스템으로 결과 반환.

### 이벤트 루프(event loop)
- 이벤트 기반 모델에서는 이벤트 루프(event loop) 라는 개념이 있다.
- 여러 이벤트가 동시에 발생했을 때 어떤 순서로 콜백 함수를 호출할지를 이벤트 루프가 판단.
- 노드는 자바스크립트 코드를 맨 위부터 한 줄씩 실행하면서 함수 호출부분이 있으면 호출 스택(call stack)에 쌓는다.
```javascript
function first() {
  second();
  console.log("First");
}

function second() {
  third();
  console.log("Second");
}

function third() {
  console.log("Third");
}

first();

// 결과 console
// Third
// Second
// First

function foo(b) {
  const a = 10;
  return a + b + 11;
  // b + 21
}

function bar(x) {
  const y = 3;
  return foo(x * y);
  // 21 + (x * 3)
}

const baz = bar(7); // 21 + 21
console.log(baz); // 42
```

### 비동기 처리
```javascript
function delayRun() {
  console.log("3초 후 실행");
}
console.log("시작");

setTimeout(delayRun, 3000);
console.log("끝");
// 결과 console
// 시작
// 끝
// 3초 후 실행
```