# 💛 Css In JS

### CSS-in-JS

CSS-in-JS란 자바스크립트를 사용하여 컴포넌트를 스타일링하는 기술이다.&#x20;

css를 작성할때는 다음과 같은 어려움점이 존재한다

CSS를 작성하는 어려움은 다음과 같다.

* Global namespace: 글로벌 공간에 선언된 이름의 명명 규칙 필요
* &#x20;Dependencies: CSS간의 의존 관계를 관리
* &#x20;Dead Code Elimination: 미사용 코드 검출
* &#x20;Minification: 클래스 이름의 최소화
* &#x20;Sharing Constants: JS와 CSS의 상태 공유
* &#x20;Non-deterministic Resolution: CSS 로드 우선 순위 이슈
* &#x20;Isolation: CSS와 JS의 상속에 따른 격리 필요 이슈

\
자바스크립트가 파싱될 때, CSS가 style 태그에 생성이 되고, DOM에 적용이 된다. \
자바스크립트를 사용하여 선언적이고 유지가능한 방식으로 스타일링을 할 수 있고,\
&#x20;컴포넌트 레벨에서의 CSS 추상화를 가능하게 한다. \
이와 같은 컨셉으로 구현되어 있는 라이브러리들이 많이 존재한다.

* Emotion
* Styled Components
* JSS
* Tailwind CSS

위와 같은 라이브러리들은 tagged template literals 문법을 사용하여 스타일 컴포넌트를 만들 수 있게 한다.

```tsx
import styled from 'styled-components';
// Create a component that renders a <p> element with blue text
const BlueText = styled.p`
  color: blue;
`;

<BlueText>My blue text</BlueText>
```

기존의 전통적인 CSS 방식과는 다르게 CSS-in-JS로는 스타일을 동적으로 만들 수 있다. \
또한 CSS를 캡슐화하여 모듈화된 코드를 작성할 수 있다.



## css-in-js의 단점

[CSS-in-JS와 성능](https://hyeonseok.com/blog/877)

[우리가 CSS-in-JS와 헤어지는 이유](https://junghan92.medium.com/%EB%B2%88%EC%97%AD-%EC%9A%B0%EB%A6%AC%EA%B0%80-css-in-js%EC%99%80-%ED%97%A4%EC%96%B4%EC%A7%80%EB%8A%94-%EC%9D%B4%EC%9C%A0-a2e726d6ace6)

1. css가 js에 포함된 경우와 파일로 분리한 경우의 성능을 비교했을 때 css in js가 성능이 더 좋지 않다.

> 실제 비교를 해본 결과 특정 사용자 인터랙션 블로킹 시간은 2배 가까이 차이가 나고 \
> 그 차이도 1초로 상당히 컸다고 한다.

2. 번들 크기를 늘린다.(styled-components는 12.7kb)
3. 리액트 devTools를 어지럽힌다, 런타임 오버헤드를 더한다.

이 외에도 많은 장단점들이 있으니 이런 장단점을 평가하고 \
해당 기술이 사용 사례에 적합한지 여부에 따라 결정을 내리는 것이 좋다.

### css-in-js의 성능 이슈에 대한 대안

* [Linaria](https://linaria.dev/)
  * CSS를 평범한 텍스트로 작성.
  * React에 종속적이지 않지만, React Styled Component도 지원함.
* [vanilla-extract](https://vanilla-extract.style/)
  * CSS를 오브젝트 형태로 표현. React의 Inline Style과 유사함.
  * React와 무관하게 사용 가능.

