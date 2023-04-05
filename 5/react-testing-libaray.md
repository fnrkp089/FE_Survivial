# 🧡 React Testing Libaray

## Enzyme&#x20;

RTL(React Testing Library)가 등장하기 전 많이 사용된 테스팅 라이브러리.\
컴포넌트의 마운트, 렌더링 및 상호작용과 관련된 테스트를 작성하는것을 도와준다.\
Enzyme은 실제 브라우저 DOM이 아닌, React가 만들어내는 가상 DOM을 기준으로 테스트를 작성해야한다.\
따라서 테스트 대상 React 컴포넌트에 어떤 prop이 넘어가고, 현재 state이 어떻게 되는지에 대해서 검증하기 용이하다.\


## React Testing Library

RTL은 실제 HTML마크업의 모습이 어떤지 테스트하기에 용이하다.

### Jest vs React Testing Library

RTL은 Jest를 포함하는 구조이고 Jest의 대안으로 나온 것이 아니다.

Jest는 테스트 실행기(test runner)와 단언 함수(assertion functions)를 제공하는 테스트 프레임워크다. Jest는 React 애플리케이션 뿐만 아니라 다른 타입의 JavaScript 코드를 테스트하기 위해 사용할 수 있다. Jest는 또한 코드 커버리지를 측정하고 모의 객체(mocks)를 생성하는 기능도 제공한다.

반면에, React Testing Library는 React 컴포넌트를 테스트하기 위한 라이브러리이다. \
RTL은 DOM에 대한 접근을 추상화하고 React 컴포넌트의 상호작용을 테스트 하기 위한 테스트 유틸리티 함수를 제공한다.\
이를 통해 개발자들은 사용자의 관점에서 애플리케이션을 테스트할 수 있습니다.

요약하면 다음과 같다.

* Jest : 자체적인 test runner와 test util 제공한다
* RTL : Jest + 리액트 컴포넌트 util 제공한다.

따라서 jest와 코드 작성 방식과 사용 방법은 매우 유사하다.\
RTL은 E2E 테스트 가까운 느낌을 주지만 브라우저에서 도는건 아니므로 E2E 테스트는 아니긴 하다.\
하지만 굉장히 빠르고, 테스트 시나리오도 쉽게 작성하기 용이하다.\


### TextField 컴포넌트 테스트 코드

```javascript
import { render, screen } from "@testing-library/react";

import TextField from "./TextField";

test("TextField", () => {
  const text = "Tester";
  const setText = () => {
    // do nothing...
  };
  // render: 테스트를 위해 컴포넌트를 jsdom에 렌더링한다.
  render(
    <TextField
      //라벨 추가
      label="Name"
      placeholder="Input your name"
      //범용적 표현으로 수정
      text={text}
      setText={setText}
    />
  );

  screen.getByLabelText("Name");
});
```

기존에 TextField 코드에는 label도 빠져있었고 text가 아니라 filterText를 사용하여 \
범용적인 표현이 아니었다.

이런 문제들을 테스트를 작성하면서 발견할 수도 있지만 \
**개발하기 전 테스트를 작성했다면 더 빨리 찾아내서 문제를 수정할수 있었을 것이다.**

시간이 지날수록, 구현의 목표는 명료한데, 시간은 짧고, 그에 비해 생각이 급해질수 있기 때문에,\
언제라도 리팩토링을 할 수 있도록 TDD를 연습해보는것이 중요하다.



## BDD

BDD(행위 주도 개발) 스타일은 소프트웨어를 테스트하고 문서화하는 방법론 중 하나이다\
TDD(테스트 주도 개발)와 유사하지만, 테스트 케이스를 작성할 때 언어적으로 이해하기 쉽게 작성한다.\
**given-when-then** 패턴과 같은 테스트 케이스 작성 방식도 BDD 스타일에 속한다. \
\
BDD에서는 비즈니스 요구사항과 소프트웨어의 동작을 명확하게 이해하고 문서화하는 것이 중요하다

## given - when - then 패턴

BDD 테스트 작성의 대표적인 예이다.

* Given : 주어진 환경을 설정(예: 검색창이 주어졌을 때)
* When : 사용자가 어떤 행위를 하는 것(예: 사용자가 검색창에 a를 입력하면)
* Then : 그에 따른 결과 정의(예: a를 인자로 setText가 실행되어야 한다)

[RTL Cheat Sheet](https://testing-library.com/docs/dom-testing-library/cheatsheet/)

## BDD 스타일로 작성한 테스트 코드

```javascript
import { fireEvent, render, screen } from "@testing-library/react";

import TextField from "./TextField";

const context = describe;

// TextField가 테스트 대상
describe("TextField", () => {
  //given : 검색창의 라벨, 상태 변수 등 테스트할 함수 안에서 주어진 환경들
  const label = "Name";
  const text = "Tester";

  const setText = jest.fn();

  //매번 실행 때마다 mock들은 초기화를 해줘야함
  beforeEach(() => {
    // setText.mockClear();
    jest.clearAllMocks();
  });

  //테스트 코드에서 반복되므로 함수로 따로 분리(관심사 분리)
  function renderTextField() {
    render(
      <TextField
        label={label}
        placeholder="input your name"
        text={text}
        setText={setText}
      />
    );
  }

  function inputText(value: string) {
    // fireEvent로 인터랙션(동작)만 검증
    // fireEvent : 쿼리 함수로 선택된 영역을 대상으로 특정 이벤트를 발생시키기 위한 이벤트 함수들을 담고 있음
    fireEvent.change(screen.getByLabelText(label), {
      target: { value },
    });
  }

  //요소들이 잘 렌더링되는지 확인
  it("renders elements", () => {
    //when : 텍스트 필드 함수를 렌더링 했을때
    renderTextField();

    //then : 라벨, placeholder, 인풋 텍스트 요소들이 화면에 잘 뜬다.
    screen.getByLabelText(label);
    screen.getByPlaceholderText(/name/);
    screen.getByDisplayValue(text);
  });
  // ------

  //when : 사용자가 검색창에 이름을 입력하면
  context("when user enters name", () => {
    beforeEach(() => {
      renderTextField();
    });
    //then : setText핸들러가 호출된다.
    it('calls "setText" handler', () => {
      inputText("New Name");
      //인자 New Name을 가지고 호출된다.
      expect(setText).toBeCalledWith("New Name");
    });
  });
});
```

그런데 우리가 지금 만들고 있는 웹은 express-demo-app에서 받아오는 데이터에 의존하고 있다. \
**실제 개발 환경에서는 이 데이터가 주어지지 않았을 수도 있고, 해당 API가 아직 완성되지 않았을수도 있으며, 테스트를 위해 계속 개발서버를 켜고 프론트 작업을 하는것은 번거로울것이다.**

****

이처럼 외부 의존성이 큰 테스트 코드를 작성한다면 해당 부분만 가짜(Mocking)를 만들어 테스트 하면 좋다.

```javascript
import { render, screen } from "@testing-library/react";

import App from "./App";

jest.mock("./hooks/useFetchProducts", () => () => [
  {
    category: "Fruits",
    price: "$1",
    stocked: true,
    name: "Apple",
  },
]);

test("App", () => {
  render(<App />);

  screen.getByText("Apple");
});

```

## Mocking 이란 ?

> 테스트할 때 외부 리소스에 의존하는 코드를 독립적으로 테스트하기 위해 가짜 객체를 만드는 기술
>
> 모킹을 사용하면 테스트가 예상대로 동작하는지 확인하기 더욱 쉽다.

**Mocking을 사용해야 하는 경우**

* 테스트할 객체가 외부 객체에 의존중인 경우
* 외부 api가 정상적으로 작동하지 않거나 호출할 때 비용이 발생하는 경우
* api 데이터가 구축되지 않은 경우

### Mock 사용 시 주의사항

* mock 객체를 불필요하게 많이 사용하면 후에 유지보수 비용이 크게 발생할 수 있다.
* 가상의 객체이므로 실제 객체로 작동했을 때 예상과 다르게 동작할 수 있다.

## Test Fixture

> 테스트 실행을 위해 베이스로 사용되는 객체들의 고정된 상태이다. 여러 테스트에서 같은 구성의 Date Set을 사용하고자 할 때 유용하다.\
> 일반적으로 테스트에 필요한 데이터나 객체, 모듈 등을 미리 생성하거나 초기화해놓은 후 테스트 케이스를 실행한다.

Test fixture를 사용하면 데이터베이스를 활용하여 테스트를 수행할 경우 \
매번 데이터 베이스를 생성하고 초기화하는 작업을 반복할 필요가 없다.

실제 react-demo-app 에서는 상품 데이터베이스가 고정적으로 필요한 상황이었다.

그래서 fixture 폴더를 만들고 그 안에 상품 객체를 만들었다.

**index.ts**

```javascript
import products from "./products";

export default {
  products,
};
```

**products.ts**

```javascript
const products = [
  {
    category: "Fruits",
    price: "$1",
    stocked: true,
    name: "Apple",
  },
];

export default products;
```

### Test Fixture 사용 예시

* Mock 또는 Fake Object의 세팅이나 생성, 삽입할 데이터가 필요한 경우
* 변하지 않으며 구체적으로 알고있는 데이터가 필요한 경우
* 특정 상태로 초기화가 필요한 객체가 존재할 경우







