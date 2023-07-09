# 🤙 Callback Function

## 콜백 함수

콜백함수는 다른 함수에 인수로 전달되는 함수입니다.  즉 함수가 실행 된 후 호출됩니다.

콜백함수는 자바스크립트에서 일반적으로 사용되는 패턴이고, 비동기 프로그래밍에서는 중요합니다.

예를들면 다음과 같은 코드를 보겠습니다.



예를 들어, 아래와 같은 코드가 있습니다:

```javascript
function greeting(name) {
  console.log('Hello ' + name);
}

function processUserInput(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
}

processUserInput(greeting);
```

이 예에서 `greeting` 함수는 콜백 함수입니다. `processUserInput` 함수는 `callback` 파라미터로 함수를 받아서, 사용자로부터 이름을 입력받은 후에 해당 콜백 함수를 호출합니다. 따라서 `greeting` 함수는 `processUserInput` 함수가 실행을 완료한 후에 호출됩니다.

콜백 함수는 이벤트 핸들러, 타이머, 비동기 요청 등 다양한 상황에서 사용됩니다.&#x20;

그러나 과도한 콜백 중첩은 "콜백 지옥"이라는 문제를 일으킬 수 있으므로 주의해야 합니다. 이런 경우에는 `Promise`나 `async/await` 같은 다른 비동기 처리 패턴을 사용하는 것이 좋습니다.



## 비동기 함수는 무조건 콜백함수?

그것은 아닙니다. 모든 비동기 함수가 콜백 함수를 사용하는 것은 이전의.이야기입니다 콜백 함수는 비동기 처리의 초기 패턴 중 하나이지만, \
지금JavaScript에서는 `Promise`와 `async/await`와 같은 다른 비동기 처리 패턴이 널리 사용됩니다.

* **콜백 함수**: 이 방법은 오래된 방식으로, 일반적으로 비동기 작업이 완료되면 호출되는 함수를 전달합니다. 이 패턴의 문제는 "콜백 지옥"이라 불리는 상황을 초래할 수 있다는 것입니다. 이는 중첩된 콜백이 많아질수록 코드가 점점 더 복잡해지고 이해하기 어려워지는 상황을 말합니다.
* **Promise**: Promise는 비동기 처리를 위한 객체로, 비동기 작업이 완료되면 결과를 "프로미스"합니다. 프로미스는 성공(fulfilled) 상태, 실패(rejected) 상태, 아직 결정되지 않은(pending) 상태를 가질 수 있습니다. `then`과 `catch` 메소드를 사용하여 프로미스의 결과를 처리할 수 있습니다. 프로미스를 사용하면 중첩된 콜백의 문제를 해결할 수 있습니다.
* **async/await**: `async/await`는 ES2017에 도입된 비동기 처리 패턴으로, 비동기 함수를 마치 동기 함수처럼 작성할 수 있게 해줍니다. `async` 함수는 항상 프로미스를 반환하며, `await` 키워드는 프로미스가 완료될 때까지 함수 실행을 일시 중지합니다. 이를 통해 비동기 코드를 깔끔하게 작성할 수 있습니다.

## Promise?

Promise는 자바스크립트에서 비동기 연산을 표현하는 객체입니다.

이 객체는 연산이 성공적으로 완료되었는지, 실패하였는지의 상태 정보를 가지고 있으며, 연산의 결과 또는 실패 이유를 값으로 가지고 있습니다. Promise는 다음의 세 가지 상태 중 하나를 가질 수 있습니다.

1. **pending**: Promise의 초기 상태로, 이행되거나 거부되지 않은 상태입니다.
2. **fulfilled**: 연산이 성공적으로 완료되었다는 것을 의미합니다.
3. **rejected**: 연산이 실패했다는 것을 의미합니다.

Promise 객체는 `then`, `catch`, `finally` 등의 메서드를 제공하여, 비동기 연산의 완료와 실패에 대한 후속 조치를 체인으로 연결할 수 있게 합니다.

```javascript
let promise = new Promise(function(resolve, reject) {
  // 비동기 작업을 수행합니다...

  if (/* 작업이 성공적으로 완료되었으면 */) {
    resolve("작업 결과");
  }
  else {
    reject(Error("작업 실패의 이유"));
  }
});

promise.then(function(result) {
  console.log(result); // "작업 결과"
}, function(error) {
  console.error(error); // Error: "작업 실패의 이유"
});
```

## Async/Await

`async/await`는 비동기 코드를 작성하는 또 다른 방법으로, ES2017에 도입되었습니다. 이는 Promise 기반의 비동기 코드를 마치 동기 코드처럼 읽히게 하여, 비동기 코드를 더 쉽게 이해하고 작성할 수 있게 해줍니다.

`async` 키워드는 함수에 붙여 비동기 함수를 선언하며, 이 함수는 항상 Promise를 반환합니다. `await` 키워드는 Promise를 기다리는 동안 실행을 일시 중지하며, Promise가 해결될 때까지 기다립니다. 이를 통해 Promise의 결과를 쉽게 추출할 수 있습니다.

```javascript
async function getPromiseResult() {
  try {
    let result = await promise; // Promise가 해결될 때까지 기다립니다.
    console.log(result); // "작업 결과"
  } catch (error) {
    console.error(error); // Error: "작업 실패의 이유"
  }
}

getPromiseResult();
```

`async/await`를 사용하면 비동기 코드를 쓰는 것이 더 간결하고 이해하기 쉬워지며, 복잡한 Promise 체인이나 중첩된 콜백을 피할 수 있습니다.

\
