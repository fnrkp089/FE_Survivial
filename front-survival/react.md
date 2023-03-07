---
description: React에 대해 간단하게 알아보자
---

# 💛 React

## React

DOM은 html, xml, CSS 등을 트리 구조로 인식하고, 데이터를 객체로 간주하고 관리한다.

React는 이 DOM Tree 구조와 같은 구조체를 Virtual DOM-가상돔으로 가지고 있다.

> _Virtual DOM은 가상의 Document Object Model을 말함._

이벤트가 발생할 때마다 Virtual DOM을 만들고, 다시 그릴 때마다 실제 DOM과 비교하고 전후 상태를 비교해, 변경이 필요한 최소한의 변경사항만 실제 DOM에 반영해,\
&#x20;앱의 효율성과 속도를 개선할 수 있음.

## Component

리액트 컴포넌트는 리액트로 만들어진 앱을 이루는 최소한의 단위라고 생각하면 편하다.\
즉 DOM구조를 만드는 틀이라고 할수있다.

\
어떤 데이터 집합을 사용하든 같은 컴포넌트를 사용하면 모두 동일한 DOM 구조가 반환되고,\
&#x20;같은 컴포넌트를 사용하면 동일한 DOM 구조를 지닌 인스턴스(instance)를 원하는 개수 만큼 만들 수 있습다.\




## Rendering

> Warning: ReactDOM.render is no longer supported in React 18. Use createRoot instead. Until you switch to the new API, your app will behave as if it's running React 17. Learn more: [https://reactjs.org/link/switch-to-createroot](https://reactjs.org/link/switch-to-createroot)

18버전부터 ReactDom.render대신 createRoot를 사용한다.

createRoot를 통해 루트를 만들어주고 렌더를 시킨다.

필요한 부분만 업데이트를 해준다.

리액트 렌더링의 기본 규칙 중 하나는 렌더링이 "순수"해야 하며 어떠한 사이드 이펙트도 없어야 한다.



### Re-Render

1. State의 변경이 감지될때 재렌더링된다
2. 부모로부터새로운 Props가 들어올시 자식 컴포넌트는 재랜더링된다
3. 부모의 props가 변경될 경우 props를 받은 자식 컴포넌트도 재렌더링된다
4. 부모 컴포넌트가 재랜더링 될때 자식 컴포넌트도 재랜더링 된다.



## 리액트 제어의 역전

리액트는 위의 렌더를 통해 어떤 방식으로 View를 업데이트 할것인지, 언제 업데이트 할것인지\
view를 정의하지않고 view가 어떻게 보일지를 선언한다.\
따라서 어떻게 보이는것인지만 선언하면, 언제 어떻게 렌더링 되는것인지 신경 쓰지 않아도 되는것이다.

또다른 예로 Redux로 언제 상태 변화가 일어나는지 리덕스가 감지하여, 화면을 업데이트 시켜주는것을 다르게 생각해보면 제어의 부분이 리덕스에게 부여된(역전)상황이다.\
IOC가 리덕스에게 적용되었다고 보면 된다.



##



