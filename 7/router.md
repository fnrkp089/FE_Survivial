# 💛 Router

이전에는 v5.0버전을 사용해서 달라진 점이 좀 많다

* Switch의 네이밍이 Routes로 변경
* exact 옵션 삭제
* component 방식 변경 (component={COM} 및 render={() => \<h1>Hello\<h1/>} 삭제)
* path를 기존의 path="/Web/:id"에서 path=":id"로, 상대 경로로 지정
* 이 외에도, path="." / path=".." 등으로 상대 경로를 표현

```javascript
// 기존
import { BrowserRouter, Route, Switch } from "react-router-dom";
import Home from "./pages/Home";
import Write from "./pages/Write";

function App() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" component={() => <Home />} />
        <Route exact path="/write" component={() => <Write />} />
        <Route component={() => <div>Page Not Found</div>} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<pre class="language-javascript"><code class="lang-javascript"><strong>//v6
</strong><strong>import React from "react";
</strong>import { BrowserRouter, Route, Routes } from "react-router-dom";
import { Main, Page1, Page2, NotFound } from "../pages";
import { Header } from ".";

const Router = () => {
  return (
    &#x3C;BrowserRouter>
      &#x3C;Header />
      &#x3C;Routes>
        &#x3C;Route path="/" element={&#x3C;Main />} />
        &#x3C;Route path="/page1/*" element={&#x3C;Page1 />} />
        &#x3C;Route path="/page2/*" element={&#x3C;Page2 />} />
        &#x3C;Route path="/*" element={&#x3C;NotFound />} />
      &#x3C;/Routes>
    &#x3C;/BrowserRouter>
  );
};

export default Router;
</code></pre>

## createBrowserRouter()

[v6.4](https://reactrouter.com/en/main/routers/picking-a-router#using-v64-data-apis)부터 추가된 Data APIs\
BrowserRouter를 생성하는 함수이며, 이를 사용하여 라우트를 정의하고 RouterProvicer를 사용해 React어플리케이션에서 라우팅을 관리할 수 있다.

> **Data API**
>
> 라우터가 렌더링하는 컴포넌트에 데이터를 전달하는 등, 데이터 불러오기와 관련된 새로운 기능들이 대거 추가 되었다.

App컴포넌트를 거치지않고 바로 브라우저 라우터를 만들경우에 사용할 수 있다

```javascript
import { createBrowserRouter, RouterProvider } from "react-router-dom";

import routes from "./routes";

const router = createBrowserRouter(routes);

root.render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

### Routes.tsx

테스트 환경에서도 라우트 정보가 필요하기때문에, 별도의 모듈로 분리해서 관리한다.

```javascript
import Layout from './components/Layout';
import HomePage from './pages/HomePage';
import DashboardPage from './pages/DashboardPage';

const routes = [
  {
    path: '/',
    element: <Layout />,
    children: [
      { index: true, element: <HomePage /> },
      { path: '/dashboard', element: <DashboardPage /> }
    ]
  }
];

export default routes;
```

### createRoutesFromElements()

createBrowserRouter()를 사용할 때 이전에 사용되던 JSX 형태로 라우터를 구성하는것이 가능하다.

```javascript
import {
  createRoutesFromElements,
  createBrowserRouter,
} from "react-router-dom";

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route
      path="/"
      element={<Root />}
      loader={rootLoader}
      action={rootAction}
      errorElement={<ErrorPage />}
    >
      <Route errorElement={<ErrorPage />}>
        <Route index element={<Index />} />
        <Route
          path="contacts/:contactId"
          element={<Contact />}
          loader={contactLoader}
          action={contactAction}
        />
        <Route
          path="contacts/:contactId/edit"
          element={<EditContact />}
          loader={contactLoader}
          action={editAction}
        />
        <Route
          path="contacts/:contactId/destroy"
          action={destroyAction}
        />
      </Route>
    </Route>
  )
);

```

## 테스트 - createMemoryRouter

테스트 환경에서는  `createBrowserRouter` 대신 `createMemoryRouter`를 사용한다.

```
import { createMemoryRouter, RouterProvider } from 'react-router-dom';

import routes from '../routes';

export function withRouter(initialEntries = '/') {

  const router = createMemoryRouter(routes, {initialEntries: [initialEntries]});
  return <RouterProvider router={router} />;
  )
}

describe('App', () => {
  it('render correctly', () => {
    render(withRouter());

    expect(screen.getByText(/스크린테스팅/)).toBeInTheDocument();
  });
});
```

