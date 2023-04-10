# 💛 MSW

## MSW(Mock Service Worker) <a href="#mswmock-service-worker" id="mswmock-service-worker"></a>

MSW는 리소스 요청을 가로채서 수정할 수 있는 `Service Worker` 의 기능 중 하나이다.\
Mock Service Worker는 `서비스 워커`를 이용하여 **API를 모킹**하는 라이브러리이다.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



### Service Worker란? <a href="#service-worker" id="service-worker"></a>

JavaScript 파일의 형태의 출처와 경로에 대해 등록하는 이벤트 기반 워커이다.

> 서비스 워커(Service Worker)는 브라우저에서 백그라운드 스크립트로 실행되는 웹 워커(worker)의 일종입니다. 서비스 워커는 브라우저와 네트워크 사이에서 중개자 역할을 하며, 브라우저와는 별개로 동작합니다.

* 워커 맥락에서 실행되므로 메인 Javascript 스레드를 방해하지 않는다.
* 네트워크 요청을 snatch해서 핸들링하므로 보안상의 위험이 있기때문에\
  HTTPS(localhost 포함)에서만 동작한다.

**Example**

* 오프라인 화면 표시 (온라인 상태일 때 offline.html을 캐싱해두고 오프라인 접속시에 해당 파일을 보여주는 형태)
* 백그라운드 데이터 동기화, 리소스의 프리페칭
* 푸시 메시지에 반응 등 (Braze service worker)
* 네트워크 요청을 가로채는 행위(MSW와 관련)
* 높은 비용의 계산을 처리할 때



## More Msw

MSW(Mock Service Worker의 약자, [https://mswjs.io](https://mswjs.io/))는 API Mocking 라이브러리로, \
서버향의 네트워크 요청을 가로채서 모의 응답(Mocked response)을 보내주는 역할을 한다.\
따라서, Mock Service Worker(MSW) 라이브러리를 통하면, \
Mock 서버를 구축하지 않아도 API를 네트워크 수준에서 Mocking 할 수 있다.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## MSW 설치

```bash
npm i -D msw
```

* jest.config.js

```javascript
module.exports = {
  testEnvironment: "jsdom",
  setupFilesAfterEnv: [
    "@testing-library/jest-dom/extend-expect",
    // 아래 속성 추가
    "<rootDir>/src/setupTests.ts",
  ],
  transform: {
    "^.+\\.(t|j)sx?$": [
      "@swc/jest",
      {
        jsc: {
          parser: {
            syntax: "typescript",
            jsx: true,
            decorators: true,
          },
          transform: {
            react: {
              runtime: "automatic",
            },
          },
        },
      },
    ],
  },
  testPathIgnorePatterns: ["<rootDir>/node_modules/", "<rootDir>/dist/"],
};
```

요청 핸들러 목록(handlers.ts), 브라우저와 서버별 설정(setupTests.ts)파일을 만드는 것을 \
**mock 정의라고 한다.** \
이 파일들은 mock 폴더를 생성 후 관리하는 것이 좋다.

src/setupTests.ts

```javascript
//fetch 함수를 제공하는 폴리필 라이브러리
import "whatwg-fetch";

import server from "./mocks/server";

// 들어오는 요청 수신 대기하도록 서버 설정
beforeAll(() => server.listen({ onUnhandledRequest: "error" }));

//모든 테스트가 완료되면 서버를 닫음
afterAll(() => server.close());

//각 개별 테스트 후 테스트끼리 영향을 주지 않도록 모의 서버 핸들러를 재설정
afterEach(() => server.resetHandlers());
```

whatwg-fetch를 가져오는 것 => 환경에서 fetch 함수를 사용할 수 있고 모의 서버에서 HTTP 요청을 가로채서 응답하는 데 사용할 수 있다.

> `whatwg-fetch`는 Fetch API를 지원하지 않는 브라우저에서 Fetch API를 사용할 수 있도록 하는 폴리필(polyfill) 라이브러리입니다. Fetch API는 브라우저에서 제공하는 네트워크 요청 기능을 제어할 수 있는 간단하고 강력한 인터페이스를 제공합니다. `whatwg-fetch`는 이를 지원하지 않는 구형 브라우저에서도 Fetch API를 사용할 수 있게끔 해주는 라이브러리로, 일반적으로 네트워크 요청에 사용됩니다.

* MSW 라이브러리로 모의 서버 설정

```javascript
import { setupServer } from "msw/node";

import handlers from "./handlers";

const server = setupServer(...handlers);

export default server;
```

* MSW 핸들러 코드 작성

handlers 파일은 express 작성 문법과 유사하다.

```javascript
import { rest } from "msw";
import fixtures from "../../fixtures";

const BASE_URL = "http://localhost:3000";

// handlers는 보통은 여러개를 작성하므로 배열의 형태임
const handlers = [
  // rest : REST api 방식으로 핸들러 작성
  // ctx: 실제로 어떻게 응답을 처리할지에 대한 세부 내용
  rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
    const { products } = fixtures;

    //
    return res(ctx.status(200), ctx.json({ products }));
  }),
];
export default handlers;
```

* App.test.ts 테스트 코드 작성

```javascript
import { render, screen, waitFor } from "@testing-library/react";
import App from "./App";

test("App", async () => {
  render(<App />);

  // 안에 있는게 될때까지 확인한다.
  // waitFor이 프로미스로 되어있어서 await 해줘야함
  await waitFor(() => {
    screen.getByText("Apple");
  });
});
```

## polyfill (폴리필)

새로운 기술이나 기능을 현재 사용 중인 브라우저에서 지원하지 않을 때, \
해당 브라우저에서 기능을 사용할 수 있도록 도와주는 코드 조각이다. \
예를 들어, ES6에서 추가된 Promise나 fetch API는 IE 11을 포함한 일부 브라우저에서 지원하지 않는다.&#x20;

\
이때, 해당 기능을 사용하고자 하는 경우 polyfill을 사용하여 브라우저가 해당 기능을 지원하지 않아도 기능을 사용할 수 있도록 할 수 있다.

폴리필을 위한 트랜스파일러에는 Babel이 있다.&#x20;

바벨이 ES6에서 추가된 모든 문법을 바꿀 수는 없다. 특히 ES5 이하를 지원하는 브라우저에서 Promise나 Set 등은 읽어낼 수가 없기 때문에 이럴 때 폴리필이 필요하다.

\


\
