# 💛 React Hook

## &#x20;React Hook&#x20;

> React v16.8에 도입됨, 기존 방식의 몇가지 문제를 해결
>
> 함수형 컴포넌트에 리액트의 다른 기능들을 **갈고리처럼 연결**해주는 역할을 하여 `Hook` 이라 명명

### Hook 탄생 배경&#x20;

#### 기존 방식의 문제점

* **Wrapper Hell(HOC)**
  * 기존 컴포넌트를 새로운 컴포넌트로 감싸서 재사용 가능한 컴포넌트를 만드는 방법
  * 훅이 나오기 이전 코드를 재사용하기 위해 사용된 방법이다.
  * 이 패턴을 남용하면, 컴포넌트의 계층 구조가 복잡해져 유지보수와 디버깅이 어려워진다.
* **Huge Components**&#x20;
  * 컴포넌트가 커질수록 클래스 내에 로직(상태, 라이프사이클 메서드)등 코드가 비대해지기 쉽다.\
    이는 가독성이 떨어지고 유지보수성을 어렵게 만든다
* **Confusing Classes**
  * 클래스의 복잡도 문제 (높은 러닝커브, this 바인딩 등)



## 동작원리

Functional Component에서 useState, useEffect와 같은 Hook 함수를 사용하면, \
React는 내부적으로 상태와 라이프사이클을 관리하기 위해 Hook 함수에 대한 **내부 연결 리스트**를 생성한다.

**Hook은 컴포넌트의 상태를 관리하므로, Hook이 호출되는 위치가 중요하다**. \
만약 Hook이 조건문이나 반복문 내부에서 호출되면,\
같은 컴포넌트의 라이프사이클에 여러번 호출될 수 있기 때문에 예기치 않은 동작을 일으킬 수 있다.

예를 들어, useEffect Hook을 사용하여 컴포넌트가 마운트될 때와 언마운트될 때 동작을 정의하였다고\
가정할시,  만약 이 Hook 함수가 조건문이나 반복문 내부에서 호출되면, 마운트와 언마운트 과정이 여러번 반복될 수 있다. \
이 경우 예상치 못한 결과가 발생할 수 있기 때문에 최상위 레벨에서만 Hook을 호출해야 한다.

**따라서, React Hook은 컴포넌트의 최상위 레벨에서만 호출되어야 하며,** \
**이를 지키지 않을 경우 예상치 못한 동작이 발생할 수 있다.**

또한  함수형 컴포넌트 내부에서만 Hook을 호출해야 하는 이유는, \
**Hook이 함수형 컴포넌트의 지역 상태를 관리하기 때문이다.**\
&#x20;함수형 컴포넌트가 렌더링될 때마다 Hook 함수가 호출되어 해당 컴포넌트의 지역 상태를 관리한다.\
&#x20;따라서, Hook이 호출되는 위치가 중요하며, 함수형 컴포넌트 내부에서만 호출해야 한다.

> 클래스형 컴포넌트에서는 이와 달리 this 키워드를 이용하여 클래스 내부에서 상태와 라이프사이클을 관리한다.\
> &#x20;함수형 컴포넌트는 클래스형 컴포넌트와 달리 인스턴스를 생성하지 않으며,\
> &#x20;this 키워드를 사용하지 않는다. \
> 따라서, 함수형 컴포넌트 내부에서만 Hook을 호출할 수 있다.

## Hooks

* **UseState**
  * 상태를 관리할 수 있게 해주는 함수,\
    컴포넌트에서 상태 값을 관리할 수 있으며, 상태 값이 변경될 때마다 컴포넌트가 다시 렌더링되어 화면에 반영됨.\
    이를 통해 React의 재사용성과 가독성을 높일 수 있습니다.
*   ****[**useEffect**](https://overreacted.io/ko/a-complete-guide-to-useeffect/)****

    * 렌더링 이후에 해야할일,  React 외부와 관련된 일을 정할 수 있다.
    * 부수 효과(side effect)를 처리할 수 있게 해주는 함수

    > 함수의 실행 결과가 함수 외부의 상태에 영향을 미치는 것을 의미합니다.&#x20;
    >
    > \
    > 예를 들어, 네트워크 요청, 타이머 설정, 이벤트 등이 부수 효과에 해당합니다.



    * 컴포넌트가 어떤 Effect를 일으키는지 초점을 맞춰 useEffect를 사용해야한다.
    * effect는 매 렌더링 후에 실행되며, 렌더링 시점의 prop과 state를 본다



### Clean-up

외부 데이터에 구독(subscription)을 설정해야 하는 경우, \
메모리 누수가 발생하지 않도록 정리(clean-up)하는 것은 매우 중요하다.\
주로 부수 효과 함수에서 등록한 이벤트 리스너나 타이머를 해제하거나, \
네트워크 요청을 취소하는 등의 작업을 수행하는데 사용된다다

```javascript
import React, { useEffect, useState } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timerId = setInterval(() => {
      setSeconds(seconds => seconds + 1);
    }, 1000);

    return () => {
      clearInterval(timerId);
    };
  }, []);

  return (
    <div>
      Seconds: {seconds}
    </div>
  );
}
```

### 의존성 배열을 이용한 fetch

useEffect의 두번째 인자로 \[]를 넣어주면 처음 한번만 실행되게 할 수 있다.

```javascript
const [products, setProducts] = useState<Product[]>([]);

useEffect(() => {
	const fetchProducts = async () => {
		const url = 'http://localhost:3000/products';
		const response = await fetch(url);
		const data = await response.json();
		setProducts(data.products);
	};

	fetchProducts();
}, []);
```

이렇게 빈 배열을 의존성 배열로 넣어주는 경우 주의해야 할 점이 있다.

의존성 배열에 필요한 값들이 없기 때문에 데이터가 변경되어도 다시 useEffect가 호출되지 않는다는 것을 알아야 한다.



```javascript
import {useEffect, useState} from 'react';
import FilterableProductTable from './components/FilterableProductTable';
import TimerControl from './components/Timer';

import Product from './types/Product';

export default function App() {
  const [products, setProducts] = useState<Product[]>([]);

  useEffect(() => {
    // Fetch
    const fetchProducts = async () => {
      const url = 'http://localhost:3000/products';
      const response = await fetch(url);
      const data = await response.json();
      setProducts(data.products);
    };

    fetchProducts();
    // 의존성 배열을 이용하면 한번만 가져온다.
  }, []);

  return (
    <div>
      <TimerControl />
      <hr />
      <FilterableProductTable products={products} />
    </div>
  );
}

```

아래처럼 의존성 배열에 userId 값을 넣어주면 userId가 변경될 때마다 useEffect의 호출이 다시 일어날 수 있다.

```javascript
useEffect(() => {
  let ignore = false;

  async function startFetching() {
    const json = await fetchTodos(userId);
    if (!ignore) {
      setTodos(json);
    }
  }

  startFetching();

  return () => {
    ignore = true;
  };
}, [userId]);
```



## useContext

Context API를 사용하기 위한 훅\
Context 객체를 사용할 수 있게 해주는 함수이다.

Context 객체는 컴포넌트 트리 상위에서 전역적으로 사용할 수 있는 데이터를 담고 있는 객체이다. Context 객체를 사용하면, 중첩된 컴포넌트들 간에 props를 계속해서 전달할 필요 없이, \
값을 직접 전달할 수 있습니다.

useContext 함수를 사용하여 Context 객체의 값을 컴포넌트 내부에서 바로 사용할 수 있다.\
useContext 함수는 Context 객체를 인자로 받아 해당 객체의 값을 반환합니다.

```javascript
import React, { createContext, useContext, useState } from 'react';

const CounterContext = createContext();

function CounterProvider(props) {
  const [count, setCount] = useState(0);
  return (
    <CounterContext.Provider value={[count, setCount]}>
      {props.children}
    </CounterContext.Provider>
  );
}

function Counter() {
  const [count, setCount] = useContext(CounterContext);
  return (
    <div>
      Count: {count}
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

function App() {
  return (
    <CounterProvider>
      <Counter />
    </CounterProvider>
  );
}
```

## useRef

변수나 DOM 요소를 저장하기 위한 훅\
상태(state)가 변경되면 해당 컴포넌트와 하위 컴포넌트를 다시 렌더링하지만, 레퍼런스 객체의 현재 값(current)이 바뀌더라도 렌더링에 영향을 주지 않는다.

ref는 DOM 노드나 컴포넌트 인스턴스와 같은 React 엘리먼트를 참조할 때 사용된다.\
&#x20;클래스형 컴포넌트에서는 `createRef()` 함수를 사용하여 ref를 생성하고,\
`ref` 속성을 사용하여 DOM 노드나 컴포넌트 인스턴스를 참조한다.\
\
**그러나 함수형 컴포넌트에서 해당 함수를 사용할 수 없기 때문에 이때 useRef 함수를 사용하여 ref 객체를 생성할 수 있다.**

useRef 함수로 생성된 ref 객체는 함수형 컴포넌트 내부에서 변경될 때마다 새로운 객체가 생성되는 것이 아니라, 같은 객체가 유지되므로, 여러 컴포넌트에서 같은 ref 객체를 사용할 수 있다.

```javascript
import React, { useRef } from 'react';

function Input() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleClick}>Focus</button>
    </div>
  );
}
```

## &#x20;useLayoutEffect

화면 성능을 높일 수 있는 훅.\
&#x20;useEffect와 비슷하지만 렌더링 전에 작업이 실행된다는 점이 다르다.

useEffect는 렌더링 후에 약속한 함수를 실행시켜주는 훅이었다. \
그래서 화면이 리렌더링될 때 useEffect로 인해 바뀐 부분은 조금 지연되어 렌더링될 수가 있었고\
사용자 입장에서는 화면 깜빡임을 느낄 수도 있다.

즉 useEffect는 렌더링 후 비동기적으로 실행되지만,\
useLayoutEffect는 렌더링 이후 동기적으로 실행한다.

**useLayoutEffect는 렌더링이 블록되므로,** \
**실행 시간이 긴 작업이 포함된 경우, 성능 문제가 발생할 수 있다.**

****

## React StrictMode

React 애플리케이션 개발 중에 발견되는 잠재적인 문제를 조기에 파악할 수 있도록 검사해주는 도구.

* 렌더링 중에 중복된 이벤트 핸들러가 실행되는 것을 방지
* 애플리케이션 내 예상치 못한 Side-Effect를 경고
* setState() 호출 시, 비동기적인 업데이트에서 발생할 수 있는 문제를 경고
* 더 상세한 오류 정보를 제공

