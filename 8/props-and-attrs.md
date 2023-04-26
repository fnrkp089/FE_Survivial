# 💙 props & attrs

### props

styled-components에서 props를 사용하면 컴포넌트 내부의 스타일을 동적으로 변경할 수 있다.&#x20;

ex)버튼 컴포넌트를 만들 때, props를 사용하여 버튼의 크기, 색상 등을 동적으로 변경할 수 있다.\
즉  styled-component는 내부적으로 props을 받을 수 있고, 그 props에 따라 스타일을 변경할 수 있다.

```js
import styled from 'styled-components';

const Button = styled.button`
  background-color: ${(props) => props.color || 'white'};
  color: ${(props) => props.textColor || 'black'};
  font-size: ${(props) => props.fontSize || '14px'};
`;

<Button color="red" textColor="white" fontSize="16px">Click Me!</Button>
```

### attrs

속성 값을 동적으로 변경하는 데 사용된다.

말 그대로 **attributes를 삽입하기 위한 메서드**이며 1개의 객체타입의 arg를 받는다



```js
const Button = styled.button.attrs(props => ({
  type: props.type || "button",
  disabled: props.disabled || false
}))`
  color: ${props => props.color || "white"};
  background-color: ${props => props.bgColor || "blue"};
  font-size: ${props => props.fontSize || "16px"};
`;
```

이 예제에서, attrs는 버튼 요소에 대한 초기 속성을 정의한다. 이 속성들은 동적으로 변경될 수 있으며, 속성에 따라 버튼의 모양과 동작이 변경될 수 있다. 예를 들어, "disabled" 속성은 버튼이 비활성화된다.

attrs는 props 객체를 받아들이고, 이를 사용하여 동적으로 속성을 설정할 수 있다. 이는 컴포넌트에 전달되는 props를 기반으로 컴포넌트의 스타일을 유연하게 제어할 수 있게 한다.

html tag가 갖고있는 고유의 attribute를 넣어 재사용하기 위한 컴포넌트를 만들 때 `attrs()`를 사용하면 유용하다.

`attrs()`의 본래의 목적은 html tag가 갖고있는 고유의 attribute를 반복적으로 사용하지 않기 위해 만들어졌다\
_ex. `<input type="checkbox" />`를 만들 때 `attrs({ type: checkbox })`를 사용_

`attrs()`이 상대적으로 `generates a CSS class`방식보다 가벼우므로 애니메이션 등의 자주 스타일이 변경되는 작업에 사용하면 효율적인 메모리 사용이 가능하다
