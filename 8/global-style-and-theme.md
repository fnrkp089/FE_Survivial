# 💜 Global Style & Theme

## css Reset

css Reset의 목표는 기본 줄 높이, 여백, 제목의 글꼴 크기 등에서 브라우저의 불일치를 줄이는 것이다.

Reset CSS를 그대로 사용하는 것은 권장하지 않으며 재설정을 하여 사용하는 것을 권장한다.

보통 styled-components를 위한 Reset CSS인 "styled-reset"을 설치해서 사용하거나 Reset Css코드를 사용한다.

```bash
npm i styled-resetnpm i styled-reset
```

```javascript
import { Reset } from "styled-reset";
import Greeting from "./components/Greeting";
import Switch from "./components/Switch";

export default function App() {
  return (
    <div>
      <Reset />
      <Greeting />
      <Switch />
    </div>
  );
}
```

## Global Style 적용

```javascript
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
	html {
		box-sizing: border-box;
	}
	
	*,
	*::before,
	*::after {
		box-sizing: inherit;
	}
	
	html {
		font-size: 62.5%;
	}
	
	body {
		font-size: 1.6rem;
	}
	
	:lang(ko) {
		h1, h2, h3 {
			word-break: keep-all;
		}
	}
`;

export default GlobalStyle;
```

App 컴포넌트에서 GlobalStyle 컴포넌트 불러오기

```javascript
import { Reset } from "styled-reset";

import GlobalStyle from "./styles/GlobalStyle";

export default function App() {
  return (
    <>
      <Reset />
      <GlobalStyle />
      <Greeting />
    </>
  );
}
```

## box-sizing 속성

요소의 크기를 계산하는 방법을 결정한다.

기본적으로, box-sizing의 값은 `content-box`로 설정되어 있다. \
이 경우에는 요소의 width와 height 속성값에는 해당 요소의 내용(content)의 크기만 포함된다. \
**즉, 테두리(border)와 안쪽 여백(padding)의 크기는 width와 height 값에 포함되지 않는다.**

box-sizing 속성값을 `border-box`로 설정하면, 요소의 width와 height 속성값에는 테두리와 안쪽 여백의 크기까지 포함된다.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### Box-sizing:

* content-box : Content 영역을 기준으로 box의 size를 적용한다.
* border-box : border 영역을 기준으로 box의 size를 적용한다.
* inherit: 부모 요소에서 상속받은 값을 사용한다.
* initial: 기본값을 사용한다.
* revert: 부모 요소에서 상속받은 값을 사용하지만, 해당 속성이 사용자에 의해 변경되었다면 그 변경된 값으로 다시 설정한다.
* revert-layer: 현재 레이어에서 가장 가까운 값으로 다시 설정한다.
* unset: 상속된 값이 있다면 상속받은 값을 사용하고, 그렇지 않다면 기본값을 사용한다.

## word-break 속성

글자가 블록 요소 내에서 줄바꿈이 될 때 단어를 분리하는 방법을 뜻한다.

**word-wrap** : 아래 예제와 같이 박스의 가로 영역을 넘친 단어 내에서 임의의 분리 여부를 결정한다.\
ex)\
[![](http://wit.nts-corp.com/wp-content/uploads/2017/06/-46)](http://wit.nts-corp.com/wp-content/uploads/2017/06/-46)

* break-all : 글자 기준으로 줄바꿈
* keep-all : 단어 기준으로 줄바꿈

## Theme

디자인 시스템의 근간을 정의한다.\
테마를  잘 정의하면 다크 모드 등에 대응하기 쉽고,  눈에 보이는 단편적인 정보를 넘어서, \
**컨텐츠의“의미”에** 집중할 수 있다.

```javascript
const defaultTheme = {
  colors: {
    background: "#FFF",
    text: "#000",
    primary: "#F00",
    secondary: "#00F",
  },
};

export default defaultTheme;
```

App 컴포넌트에서 `ThemeProvider`의 props로 `defaultTheme`를 넘겨준다.

```javascript
import { ThemeProvider } from "styled-components";
import { Reset } from "styled-reset";
import defaultTheme from "./styles/defaultTheme";
import GlobalStyle from "./styles/GlobalStyle";

export default function App() {
  return (
    // ThemeProvider를 통해 아래에 있는 모든 컴포넌트에 theme 전달
    <ThemeProvider theme={defaultTheme}>
      <Reset />
      <GlobalStyle />
      <Greeting />
    </ThemeProvider>
  );
}
```

`defaultTheme`의 타입을 잡아주기 위해 Theme.ts 파일을 하나 더 만든다.

```javascript
import type defaultTheme from "./defaultTheme";

type Theme = typeof defaultTheme;

export default Theme;
```

styled-compnents 모듈의 기본 테마가 Theme 타입을 상속하도록 정의한다.\
즉  이미 존재하는 타입들에 추가적인 타입을 선언할 수 있도록 하자.

```javascript
import 'styled-components';

import type Theme from './Theme';

declare module 'styled-components' {
    export interface DefaultTheme extends Theme {}
}

```

기본 테마를 바탕으로 다크테마를 만드는것도 쉽다.

```javascript
import type Theme from "./Theme";

const darkTheme: Theme = {
  colors: {
    background: "#000",
    text: "#FFF",
    primary: "#F00",
    secondary: "#00F",
  },
};

export default darkTheme;
```

App에서 useDarkMode() 훅을 활용하면 더 쉽게 다크모드를 구현할 수 있다.

```javascript
import { useDarkMode } from "usehooks-ts";
import { Reset } from "styled-reset";
import { ThemeProvider } from "styled-components";

import defaultTheme from "./styles/defaultTheme";
import darkTheme from "./styles/darkTheme";

import GlobalStyle from "./styles/GlobalStyle";

import Greeting from "./components/Greeting";
import Switch from "./components/Switch";
import Button from "./components/Button";

export default function App() {
  const { isDarkMode, toggle } = useDarkMode();

  const theme = isDarkMode ? darkTheme : defaultTheme;

  return (
    <ThemeProvider theme={theme}>
      <div>
        <Reset />
        <GlobalStyle />
        <Button onClick={toggle} active={isDarkMode}>
          Toggle Dark Mode
        </Button>
        <Greeting />
        <Switch />
      </div>
    </ThemeProvider>
  );
}
```

