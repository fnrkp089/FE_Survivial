# 🧡 Routes

## 라우터란?

> 웹 어플리케이션에서 라우터는 사용자의 요청을 처리하고 해당 요청에 따른 적절한 페이지나 콘텐츠를 제공하는 기능을 담당하는 프로그램이다.

순수 바닐라 JS에선 첫 번째는 Fragment 해시를 이용하는 방법(해시 라우터)과 두 번째는 history API를 이용하는 방법(브라우저 라우터)이 있다. \
history API인 [pushState와 popState 메서드가 지원](https://caniuse.com/?search=history%20api)되면서,\
&#x20;Fragment 해시를 쓰지 않고도 라우팅 시스템을 개발할 수 있게 되었다

리액트에서는 React-router-dom으로 라우팅 기능을 구현할 수 있다.

**Routes** : 자식 route들을 구성하고 있는 단위이다.

```javascript
import { Routes, Route } from "react-router-dom";

function App() {
  return (
    <div>
      <Header />
      <main>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/about" element={<AboutPage />} />
        </Routes>
      </main>
      <Footer />
    </div>
  );
}
```

## React Router

리액트 라우터는 "client side routing"(CSR)을 가능하게 한다.

또한 SPA방식이다.

> SPA는 Single Page Application으로 페이지가 한 개인 웹 어플리케이션을 의미한다. \
> 즉 기존의 웹페이지 처럼 여러개의 페이지를 사용ㅎ는것이 아니라 하나의 페이지 안에서 필요한 데이터만 가져오는 형식이다.

```
npm i react-router-dom
```

```typescript
import { Routes, Route } from "react-router-dom";

import HomePage from "./pages/HomePage";
import Aboutpage from "./pages/AboutPage";
import Header from "./components/Header";
import Footer from "./components/Footer";

const pages = {
  "/": HomePage,
  "/about": Aboutpage,
};
export default function App() {
  const path = window.location.pathname;

  const Page = Reflect.get(pages, path) || HomePage;

  return (
    <div>
      <Header />
      <main>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/" element={<HomePage />} />
        </Routes>
        <Page />
      </main>
      <Footer />
    </div>
  );
```

위의 경우, 로컬의 환경에서 테스트 할때는 오류가 나기 때문에 웹브라우저 환경과 똑같은 형식을 잡아주자.

#### Browser Router

`<BrowserRouter>`는 URL을 사용하여 브라우저의 주소창에 현재 위치를 저장하고 브라우저에 내장된 history 스택을 사용하여 탐색한다.

HTML의 history api를 사용해 클라이언트 측 라우팅을 처리한다. \
리액트에서 react-router-dom을 사용하려면 BrowserRouter 컴포넌트로 감싸줘야 한다.\
그러면 페이지 전환을 감지하고, url 경로를 업데이트하여 해당 경로에 매칭되는 컴포넌트를 렌더링 시킬 수 잇게 된다

* URL과 매핑되는 페이지 컴포넌트를 렌더링한다
* history 객체를 사용해서 뒤로가기, 앞으로가기, 새로고침등의 동작을 처리할수있다.

```js
import { BrowserRouter, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Route path="/" exact component={Home} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
    </BrowserRouter>
  );
}
```

```typescript
import "reflect-metadata";

import App from "./App";
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";

function main() {
  const element = document.getElementById("root");

  if (!element) {
    return;
  }

  const root = ReactDOM.createRoot(element);

  root.render(
    <React.StrictMode>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </React.StrictMode>
  );
}

main();
```

#### [Memory Router](https://reactrouter.com/en/main/router-components/memory-router)

브라우저의 url을 변경하지 않고, 메모리 내에서 라우팅을 처리한다.\
`<BrowserHistory>` 및 `<HashHistory>`와 달리 브라우저의 히스토리 스택과 같이 외부 소스에 연결되지 않는다.\
따라서 테스트와 같이 히스토리 스택을 완벽히 제어해야할 경우의 시나리오에 이상적인 방식이다.

테스트나 서버 사이드 렌더링에서 유용하게 사용되는데 테스트에서는 브라우저가 없어도 동작하는 메모리 내 라우팅을 사용하여 더 쉽게 테스트할 수 있다.

```typescript
import { render, screen } from "@testing-library/react";

import { MemoryRouter } from "react-router-dom";

import App from "./App";

const context = describe;

describe("App", () => {
  context('when the current path is "/"', () => {
    it("renders the home page", () => {
      render(
        <MemoryRouter initialEntries={["/"]}>
          <App />
        </MemoryRouter>
      );

      screen.getByText(/Home/);
    });
  });
  context('when the current path is "/about"', () => {
    it("renders the about page", () => {
      render(
        <MemoryRouter initialEntries={["/about"]}>
          <App />
        </MemoryRouter>
      );

      screen.getByText(/This is test/);
    });
  });
});
```
