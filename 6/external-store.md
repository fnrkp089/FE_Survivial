# ❤ External Store

## External Store

리액트에서 External Store는 보통 상태 관리 라이브러리인 Redux, MobX, Recoil 등을 이용하여 구현되는 전역 상태 관리 장치를 의미한다

즉 UseState와 같이 내부가 아닌 외부에 상태관리를 위임하고 해당 스토어를 우리가 구독(subscribe)하게된다\
이렇게 구독하고 있을때, 해당 스토어의 상태가 변경되면, 자동으로 감지하고 처리하게 된다.

리액트에서 컴포넌트 상태가 변경되면 해당 컴포넌트를 다시 렌더링하는 방식으로 상태 관리를 한다. \
그런데 상태가 너무 많고 복잡해지면 컴포넌트 간에 상태 전달이 복잡해지고 유지보수도 어렵다.&#x20;

이 때 external store를 이용하여 전역에서 상태를 관리한다,상태가 변경될때마다 \
모든 구독자들에게 알리고 업데이트를 할 수가 있게된다

외부에서 상태를 관리하는 것이지만 실제로는 external store가 가장 안쪽에 있다고 봐야하며, 신경을 많이 써야한다.



## 관심사 분리

보통 리액트 애플리케이션은 여러 컴포넌트로 이루어져 있고 각 컴포넌트는 특정 역할과 책임을 가진다. 이 때 각 컴포넌트들이 다른 컴포넌트와 의존하지 않도록 구현하기 위해서 관심사의 분리를 해야한다.

### 기능별

App

* Header
* Main
* Greeting
* Counter
* Post
* PostForm -TextField
* Footer

### 아키텍쳐 관점

흔히 사용되는 Layered Architecture에서는 사용자한테 가까운것(ui)\
먼 것(business logic)를 기준으로 관심사를 구분한다.

사람 - 스위치 -> 모터 -> 바퀴

* 스위치의 관심사 : 켜고 껐을 때 동작하는지 안하는지만 관심을 가진다.
* 모터 : 전류가 흐르면 돌기만 하면된다. 전류에 대한 관심만 가진다.

### Layerd Architecture

Layered Architecture(계층형 아키텍처)는 소프트웨어 시스템을 일련의 계층으로 분할하는 \
아키텍처 패턴이다. \
각 계층은 독립적으로 동작하며, 상위 계층은 하위 계층에 의존한다.\
이러한 계층 구조를 통해 시스템의 복잡성을 줄이고, 유지보수성과 확장성을 높일 수 있다.

* Presentation Layer : 사용자 인터페이스(ui)가 주 관심사이다. 비즈니스 로직이 어떻게 수행되는지는 알 필요가 없다. 웹 애플리케이션에서는 HTML, CSS, JavaScript로 작성된 클라이언트 측 코드가 이 계층이다.\

* Business Layer : persistence 계층에서 데이터를 가져와서 비즈니스 로직을 수행하고 그 결과를 presentatoin 계층으로 전달한다.\

* Persistence Layer : 데이터 출처와 그 데이터를 가져오고 다루는 것이 주 관심사이다.\

* Database Layer : 이터와 관련된 계층으로, 데이터베이스와의 상호작용을 처리한다. 이 계층에서는 데이터베이스와의 연결, 쿼리 수행, 데이터 변환 등을 수행한다.

Layered Architecture는 계층 간의 인터페이스를 명확히 정의하여 각 계층을 독립적으로 개발하고, 테스트할 수 있도록 한다.\
또한 계층 간의 의존성을 최소화함으로써, 하위 계층의 변경이 상위 계층에 영향을 주지 않도록 한다.\
이러한 특징들은 소프트웨어의 유지보수성과 확장성을 높이는 데 중요한 역할을 한다.

그리고레이아웃 아키텍쳐에서 각각 나누어진 계층들은 수직적으로 배치된다. \
이것 또한 주요한 특징 중 하나이다. 이 구조에서 특정 레이어는 바로 하위 레이어에만 연결되고 특정 레이어는 다른 레이어의 내부 동작을 모르게 된다.

즉, 각 계층은 캡슐화되어있고 단일 책임을 갖는다.

## Flux Architecture

Flux Architecture는 Facebook에서 개발한 React.js의 상태 관리 패턴 중 하나이다. \
React.js는 UI를 컴포넌트 단위로 관리하고, 컴포넌트 간의 데이터 흐름을 단방향으로 유지하는데, \
Flux Architecture는 이러한 데이터 흐름을 관리하는 데에 중점을 둡니다.

Flux Architecture는 다음과 같은 구성 요소로 이루어져 있다.

1. Dispatcher: 액션(Action)을 전달하고, 스토어(Store)에 알림을 보내는 중앙 집중형 허브\
   \-  내부에 상태 관리 로직은 없고 .store간 의존성을 관리한다.
2. Action: 사용자의 입력 또는 시스템 이벤트와 같은 작업을 수행하는 데 필요한 정보를 전달하는 객체\
   \- 액션 이름(type)이 담겨있고 데이터는 payload에 담긴다. store가 dispatcher에 등록해둔\
   &#x20;  콜백 함수를 통해 모든 action이 store로 전달된다.
3. Store: 애플리케이션의 상태를 저장하는 곳으로, Dispatcher로부터 액션을 받아서 처리하고, 변경된 상태를 View에 전달\
   \- Dispatcher에서 전달된 Action을 통해 상태를 변경하고, 변경될경우  View에 알린다.
4. View: UI를 구성하는 컴포넌트. 사용자의 입력에 대한 액션을 생성하고, 상태 변화를 감지하여 화면을 업데이트\
   \- controller-view 역할 두가지를 동시에 한다. 변경 이벤트를 듣는 controller-view가 자식 view에게         새로운 데이터를 제공한다. store에서 전달받은 변경된 상태를 화면에 렌더링한다. 사용자에 의해 상   태가 변경되면 또 수신하고 dispatcher에 action을 전달하기도 한다.



Flux Architecture에서는 **데이터 흐름이 단방향으로 유지되며,**\
**Dispatcher와 Store는 중앙 집중형으로 상태를 관리한다.**\
이러한 구조는 복잡한 애플리케이션에서도 상태 관리를 간단하게 유지할 수 있도록 하며, 코드의 예측 가능성과 유지보수성을 높이는 데에 도움이 된다. \
또한, 여러 컴포넌트에서 동일한 데이터를 공유할 때 유용하며, 애플리케이션 규모가 커질수록 그 효과가 더욱 용이하다.

다만, **작은 기능을 위해 초기에 많은 코드들을 작성하게되어 오버 프로그래밍의 위험성이 존재한다.**\
그렇기 때문에 Redux와 같은 상태 관리 도구들이 등장하기 시작한다.

## useReducer

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);

//reducer는 이러한 함수임
function reducer(state) {
  return state + 1;
  // 상태의 초기값이 있으면
  // return {...state, x: x + 1};
}
```

useReducer는 useState의 대체 함수이다. 아래는 useState로 만들었던 counter를 reducer를 사용해서 만든 코드이다.

```javascript
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  // dispatch에 action type을 전달
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}
```

useReducer의 첫 번째 인자로 reducer함수를 전달해주고 두 번째 인자로 리듀서의 기본값인 {count: 0}을 넣어준다.

dispatch함수에 action을 전달하면 리듀서 함수가 호출되는 구조이다.

상태를 어떻게 바꾸는지에 대한 비즈니스 로직이 리액트 컴포넌트 외부로 분리될 수 있다는 것이 장점이다.

## useCallback

useCallback을 이용하면 함수가 변경될 때만 새로 렌더링 해줄 수가 있다. 그렇기 때문에 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용한다.



