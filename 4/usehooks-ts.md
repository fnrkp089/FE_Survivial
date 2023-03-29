# 💚 Usehooks-Ts

usehooks-ts는 타입스크립트로 작성된 React Hook 라이브러리이다.

[usehooks-ts](https://usehooks-ts.com/)

## usehooks-ts 설치

```bash
npm i usehooks-ts
```

## useBoolean / useCounter

참 / 거짓을 다루는 토글 같은 경우에는 명확한 함수를 쓰는 것이 더 좋다.

기존에 만들었던 react-demo-app에서도 토글기능으로 useState를 사용했었는데 useBoolean을 사용하면 훨씬 더 코드가 명확해진다.

```javascript
import { useEffect, useRef, useState } from "react";

import { useBoolean, useCounter } from "usehooks-ts";

import useFetchProducts from "../hooks/useFetchProducts";

function Timer() {
  useEffect(() => {
    const savedTitle = document.title;
    const id = setInterval(() => {
      document.title = `Now: ${new Date().getTime()}`;
    }, 100);

    return () => {
      clearInterval(id);
      document.title = savedTitle;
    };
  });

  return <p>Playing</p>;
}

export default function TimerControl() {
  //useBoolean 사용
  const { value: playing, toggle: togglePlaying } = useBoolean();
  const { count, increment } = useCounter(0);

  return (
    <div>
      {playing ? <Timer /> : <p>stop</p>}
      <button type="button" onClick={togglePlaying}>
        Toggle
      </button>
      <p>{count}</p>
      <button type="button" onClick={increment}>
        Increase
      </button>
    </div>
  );
}
```

counter도 useState를 useCounter로 바꿔주었다.

## useEffectOnce

useEffect 안에서 데이터를 받아오는 비동기 함수를 작성한다\
useEffect의 두번째 인자로 의존성 배열을 빈 배열로 넣어주면 한번만 실행하도록 유도하는데,\
useEffectOnce를 사용할경우,  useEffect를 한 번만 실행하도록 도와준다\
useEffectOnce를 사용하면, 컴포넌트가 처음 렌더링될 때만 useEffect 함수가 실행된다.

```javascript
import { useState } from 'react';
import { useEffectOnce } from 'usehooks-ts';
import type Product from '../types/Product';

export default function useFetchProducts() {
  const [products, setProducts] = useState<Product[]>([]);

  useEffectOnce(() => {
    // Fetch
    const fetchProducts = async () => {
      const url = 'http://localhost:3000/products';
      const response = await fetch(url);
      const data = await response.json();
      setProducts(data.products);
    };

    fetchProducts();
  });

  return products;
}

```

## useFetch

useFetch를 사용하면, |\
API 요청 결과를 받아와서 상태로 관리할 수 있으며, \
이를 화면에 출력할 수 있다다\
. 다음은 useFetch의 예시입니다.

```javascript
export default function useFetchProducts() {
  const url = "http://localhost:3000/products";
  const { data } = useFetch(url);

  if (!data) {
    return [];
  }

  return data.products;
}
```

## useInterval

일정한 시간 간격으로 작업을 수행하고 싶을 때 사용한다.

useInterval을 사용하면, \
setInterval 함수를 사용하여 작업을 주기적으로 실행할 수 있으며, \
컴포넌트가 마운트되고 언마운트될 때 자동으로 작업을 시작하거나 중지할 수 있다.

첫번째 인자로 콜백 함수를, 두번째 인자로 시간 간격을 입력받는다.

아래는 useInterval을 이용하여 입력받은 지연시간마다 count를 증가시키는 예제이다.

```javascript
import { ChangeEvent, useState } from "react";

import { useInterval } from "usehooks-ts";

export default function Component() {
  // The counter
  const [count, setCount] = useState < number > 0;
  // Dynamic delay
  const [delay, setDelay] = useState < number > 1000;
  // ON/OFF
  const [isPlaying, setPlaying] = useState < boolean > false;

  useInterval(
    () => {
      // 3. delay 시간마다 이 콜백 함수가 실행된다.
      setCount(count + 1);
    },
    // 2. isPlaying이 true가 되어 input창에서 입력한 delay 값이 들어온다.
    isPlaying ? delay : null
  );

  const handleChange = (event: ChangeEvent<HTMLInputElement>) => {
    setDelay(Number(event.target.value));
  };

  return (
    <>
      //4. count의 상태가 변할때마다 리렌더링
      <h1>{count}</h1>
      // 1. play 버튼을 누르면 isPlaying의 상태가 변한다.
      <button onClick={() => setPlaying(!isPlaying)}>
        {isPlaying ? "pause" : "play"}
      </button>
      <p>
        <label htmlFor="delay">Delay: </label>
        <input
          type="number"
          name="delay"
          onChange={handleChange}
          value={delay}
        />
      </p>
    </>
  );
}
```

useInterval 함수는 컴포넌트가 마운트될 때 자동으로 작업을 시작하며, \
컴포넌트가 언마운트될 때 자동으로 작업을 중지한다. \
이를 통해, setInterval 함수를 사용할 때 발생할 수 있는 메모리 누수나 예기치 않은 작업을 미연에 방지할 수 있다.

## useEventListener

이벤트 리스너를 등록하는 커스텀 훅이다. 기본적으로 addEventListener와 removeEventListener 함수를 사용하여 이벤트를 등록하고 제거한다.

useEventListener는 특정 DOM 요소에 대한 이벤트 처리를 단순화하고, React의 라이프사이클 메서드와 함께 사용하기에도 좋다. 이를 통해 이벤트 처리와 관련된 코드를 깔끔하고 재사용 가능한 함수로 만들 수 있다.

useEventListener 훅은 다음과 같은 매개변수를 받는다.

* eventName: 등록할 이벤트 이름
* handler: 이벤트 핸들러 함수
* element: 이벤트를 등록할 DOM 요소 (기본값: window)
* options: 이벤트 등록에 대한 옵션 객체 (기본값: {})

```javascript
import { useRef } from "react";

import { useEventListener } from "usehooks-ts";

export default function Component() {
  // Define button ref
  const buttonRef = useRef < HTMLButtonElement > null;
  const documentRef = useRef < Document > document;

  const onScroll = (event: Event) => {
    console.log("window scrolled!", event);
  };

  const onClick = (event: Event) => {
    console.log("button clicked!", event);
  };

  const onVisibilityChange = (event: Event) => {
    console.log("doc visibility changed!", {
      isVisible: !document.hidden,
      event,
    });
  };

  // 스크롤 이벤트가 발생하면 실행
  useEventListener("scroll", onScroll);

  // 브라우저 탭의 컨텐츠가 visible 또는 hidden 상태로 변화할 때 발생
  useEventListener("visibilitychange", onVisibilityChange, documentRef);

  // 클릭 이벤트가 발생하면 실행
  useEventListener("click", onClick, buttonRef);

  return (
    <div style={{ minHeight: "200vh" }}>
      <button ref={buttonRef}>Click me</button>
    </div>
  );
}
```

## useLocalStorage

LocalStorage에 데이터를 저장하고 불러오기 위해 사용된다.

useLocalStorage는 useState와 useEffect를 사용하여 구현한다. \
.useLocalStorage을 사용하면, 로컬 스토리지에 데이터를 저장하고, \
데이터를 가져와서 사용할 수 있다.

useLocalStorage를 사용하면 브라우저의 LocalStorage를 쉽게 다룰 수 있어서, 로그인 상태나 사용자의 기본 설정 등을 저장하는 데 유용하다.

```javascript
import { useLocalStorage } from "usehooks-ts";

// Usage
export default function Component() {
  const [isDarkTheme, setDarkTheme] = useLocalStorage("darkTheme", true);

  const toggleTheme = () => {
    setDarkTheme((prevValue: boolean) => !prevValue);
  };

  return (
    <button onClick={toggleTheme}>
      {`The current theme is ${isDarkTheme ? `dark` : `light`}`}
    </button>
  );
}
```

이 기능은 새로고침을 하여 리렌더링을 해도 localStorage에 테마 정보가 들어있기 때문에 초기화되지 않는다.



## useDarkMode

다크 모드 기능을 간편하게 구현할 수 있도록 도와주는 Hook 함수이다.

\
useDarkMode 함수는 두 개의 매개변수를 받는다.\
&#x20;첫 번째 매개변수는 다크 모드 설정에 사용될 CSS 클래스 이름이며, \
두 번째 매개변수는 초기값으로 다크 모드를 사용할지 여부이다.

```javascript
import { useDarkMode } from "usehooks-ts";

export default function Component() {
  const { isDarkMode, toggle, enable, disable } = useDarkMode();

  return (
    <div>
      <p>Current theme: {isDarkMode ? "dark" : "light"}</p>
      <button onClick={toggle}>Toggle</button>
      <button onClick={enable}>Enable</button>
      <button onClick={disable}>Disable</button>
    </div>
  );
}
```

## swr(Stale-While-Revalidate)

swr은 Next.js팀에서 만든애플리케이션에서 데이터를 쉽게 관리하고 캐싱할 수 있는 라이브러리이다.\
\
swr은 사용하기 쉽고 간편하며, 다음과 같은 특징을 가지고 있다.

> * 자동 캐싱: swr은 데이터를 가져와서 자동으로 캐시에 저장합니다. 캐시된 데이터는 나중에 다시 사용할 수 있으며, 캐시 유효기간이 지나면 데이터를 다시 가져옵니다.
> * 즉시 렌더링: swr은 캐시된 데이터를 먼저 보여주고, 백그라운드에서 데이터를 업데이트합니다. 이를 통해 사용자 경험을 개선하고, 데이터 로딩 시간을 최소화할 수 있습니다.
> * 에러 핸들링: swr은 데이터를 가져오는 중에 발생하는 에러를 쉽게 핸들링할 수 있습니다. 에러가 발생하면, swr은 에러 메시지를 표시하거나, 이전에 캐시된 데이터를 보여줍니다.

잘 변경되지 않는 데이터(영화 정보, 회원 정보 등)에 대해 클라이언트 측에서 자주 호출할 필요가 없다. 그래서 swr과 같은 라이브러리를 사용해서 서버 측에서 필요할 때만 데이터를 호출하고 최신 데이터를 유지하면서 성능을 최적화 할 수 있다.

```jsx
import useSWR from "swr";

function Profile() {
  const { data, error } = useSWR("/api/user", fetch);

  if (error) return <div>failed to load</div>;
  if (!data) return <div>loading...</div>;

  return <div>hello {data.name}!</div>;
}
```

swr은 서버 사이드 렌더링(SSR)을 지원하며, 다양한 플랫폼에서 사용할 수 있습니다.\
&#x20;swr은 Next.js, React Native, Vue.js 등의 프레임워크에서도 사용할 수 있으며, \
다양한 백엔드와 연동하여 사용할 수 있다.

## React Query

Tanner Linsley가 만든 라이브러리로, 여러 API 요청을 관리하고 캐싱한다.\
swr과 유사한 기능을 제공하며, 데이터를 쉽게 캐싱하고, 캐시된 데이터를 빠르게 가져올 수 있다.\
또한 서버와의 상호작용을 단순화하고 최적화하는 것이 목적이다.

Axios, Fetch, GrapQL, REST API와 함께 사용할 수 있다.

```jsx
import { useQuery } from "react-query";

function Profile() {
  const { data, isLoading, error } = useQuery("user", () =>
    fetch("/api/user").then((res) => res.json())
  );

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Failed to load</div>;

  return <div>Hello {data.name}!</div>;
}
```

리액트 쿼리는 캐싱 기능을 사용하여 이전에 요청한 데이터를 캐싱하고, 데이터가 변경되지 않으면 이전 캐시된 데이터를 사용한다.

> 두 라이브러리 모두 서버와의 상호작용을 간단하고 효율적으로 만들어주고, 캐싱을 통해 성능을 향상시키며, 여러 상황에서 유연하게 대처할 수 있도록 도와준다. \
> 하지만 SWR은 데이터를 가져오는 데 초점을 맞추고, React Query는 데이터 관리와 캐싱에 초점을 맞추고 있다는 차이가 있다.
