# 💚 Navigation

## Web APIs - History

DOM Window 객체는 history 객체를 통해 browser의 session 기록을 제공한다.\
브라우저에서 뒤로 이동하거나 앞으로 이동하는 것을 가능하게 하는 메서드와 프로퍼티들이 존재한다.

history 객체는 스택과 비슷한 형태로 되어있는데 \
`pushState()` 메서드와 `replaceState()` 메서드는 히스토리를 수정하고 추가할 수 있다.

## History.pushState()

History.pushState 는 페이지 이동 없이 주소만 바꿔준다. (브라우저의 뒤로가가 버튼이 활성화 된다.)

브라우저 페이지를 이동하게 되면 window.onpopstate 라는 이벤트가 발생하게 되는데, pushState 를 했을때는 popstate 이벤트가 발생하지않고, 뒤 / 앞으로 가기를 클릭 했을때 popstate 이벤트가 발생하게 된다.

즉, pushState 와 popstate 둘을 이용하여 SPA 의 페이지 전환을 구현할 수 있다.

```javascript
import { SyntheticEvent } from "react";

export default function Header() {
  const handleClick = (event: SyntheticEvent) => {
    event.preventDefault();
    const state = {};
    const title = "";
    const url = "/about";
    history.pushState(state, title, url);
  };

history.pushState(state, title, url);
return (
    <header>
      <nav>
        <ul>
          <li>
            <a href="/" onClick={handleClick}>
              Home
            </a>
          </li>
          <li>
            <a href="/about" onClick={handleClick}>
              About
            </a>
          </li>
        </ul>
      </nav>
    </header>
  );


```

## Link

`<Link>`는 사용자가 클릭하거나 탭하여 다른 페이지로 이동할 수 있게 해주는 요소다.\
&#x20;리액트 라우터 돔에서 `<Link>`는 링크하는 리소스를 가리키는 \
실제 href가 있는 접근 가능한 `<a>` 엘리먼트를 렌더링한다.

```javascript
import { Link } from "react-router-dom";

export default function Header() {
  return (
    <header>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
        </ul>
      </nav>
    </header>
  );
}
```

### Route와 Path

> dynamic segments를 사용하는 경우 차이가 나타난다.\
> 현재 경로가 '/product/:id', 즉 '/product/1234'라고 한다면&#x20;
>
> * \<LInk to='/comment' relative='route'> 인 경우 '/product/1234/comment' 로 이동된다.
> * \<LInk to='/comment' relative='path'> 인 경우 '/product/comment' 로 이동된다.

## Navigate

`<Navigate>` 요소는 렌더링될 때 현재 위치를 변경한다. \
useNavigate를 둘러싼 컴포넌트이고, 프로퍼티와 동일한 인수를 모두 허용한다.

특정페이지로 무조건 이동하게하는 이벤트와 같은것은, Navigate를 이용하여 만들 수 있다.

예를들어 로그아웃후, 홈으로 이동하게 할때

```javascript
import { Navigate } from "react-router-dom";

export default function LogoutPage() {
  return <Navigate to="/" />;
}
...
import HomePage from "./pages/HomePage";
import AboutPage from "./pages/AboutPage";
import LogoutPage from "./pages/LogoutPage";
import Layout from "./Layout";

const routes = [
  {
    element: <Layout />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/about", element: <AboutPage /> },
      { path: "/logout", element: <LogoutPage /> },
    ],
  },
];

export default routes;
```

## useNavigate

페이지 이동 후 Navigate로 리다이렉트 할 필요없이

바로 이동하는 경우 사용할 수 있다.

```javascript
import { useNavigate } from "react-router-dom";

export default function Footer() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate("/about");
  };

  return (
    <footer>
      <button type="button" onClick={handleClick}>
        Press
      </button>
    </footer>
  );
}
```
