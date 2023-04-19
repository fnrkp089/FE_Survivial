# ❤ Routing

## HTML DOM API

HTML DOM API를 이용하면 DOM 요소에 접근 및 제어가 가능하고 Form 데이터라던지, 브라우저 히스토리에 대한 정보 접근 등이 가능하다.

이 중에서 우리는 History API 의 location이라는 인터페이스를 사용하면 url을 알 수 있다. document.location이나 window.location을 통해 접근할 수 있다.

## Location

`Window.location` 프로퍼티를 사용하여 읽기 전용객체인 location객체를 얻을수 있다.

(예제 도메인)&#x20;

http://www.example.com:8080/search?q=devmo#test

#### Location의 properties

| Property  | Description                | Example                                         |
| --------- | -------------------------- | ----------------------------------------------- |
| hash      | 주소값에 붙어있는 anchor값 반환       | #test                                           |
| host      | URL의 도메인과 포트 반환            | www.example.com:8080                            |
| hostname  | URL의 도메인 반환                | www.example.com                                 |
| href      | URL 반환                     | http://www.example.com:8080/search?q=devmo#test |
| orgin     | 프로토콜 + URL의 도메인 + 포트       | http://www.example.com:8080                     |
| pathname  | URL 경로 반환                  | /search                                         |
| port      | 서버 포트 반환                   | 8080                                            |
| protocol  | 프로토콜 반환                    | http:                                           |
| search    | URL에 붙은 매개변수 반환(물음표 뒤의 값)  | ?q=devmo                                        |

\
강의 코드

App.tsx

```javascript
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
        <Page />
      </main>
      <Footer />
    </div>
  );
}
```

./pages/Header.tsx

```javascript
export default function Header() {
  return (
    <header>
      <nav>
        <ul>
          <li>
            <a href="/">Home</a>
          </li>
          <li>
            <a href="/about">About</a>
          </li>
        </ul>
      </nav>
    </header>
  );
}
```

./pages/Footer.tsx

```javascript
export default function Footer() {
  return (
    <footer>
      <hr />
      Footer
    </footer>
  );
}
```

./components/AboutPage.tsx

```javascript
export default function Aboutpage() {
  return (
    <div>
      <h1>About</h1>
      <p>This is test</p>
    </div>
  );
}
```

./components/HomePage.tsx

```javascript
export default function HomePage() {
  return (
    <div>
      <h1>Welcome!</h1>
      <p>Hello, world</p>
    </div>
  );
}
```
