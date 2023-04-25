# 🧡 Style Basics

의미있는 마크업을 하기 위해서는 `HTML Element 들이 어떤 의미를 가지고 있는지` \
정확하게 알고 있어야 한다.

## className

jsx에서 html에 class를 넣을 때는 className을 사용해야 한다.

자바스크립트에서 class는 예약어이기 때문에 className이라고 쓴다.

## getElementsByClassName()&#x20;

\
이 함수는 태그의 class="" 속성을 사용하여 접근한다.\
동일한 class명이 존재할수 있기때문에  ( id속성은 html 문서에 동일한 id속성이 존재하면 안된다..) \
id 속성을 사용하여 접근하는 getElementById() 와 달리 getElementsByClassName() 은 컬렉션 객체를 반환한다.\
따라서 for문을 사용하거나 특정 index에 위치한 element를 반환받아 사용할수있다.

### 시맨틱 태그

시맨틱(semantic)이라는 '의미의', '의미론적인'라는 뜻을 가진 형용사이다.\
즉 시맨틱 태그는 의미를 부여한 태그라는 뜻이 됩니다.

태그에 의미를 부여했다고 생각하시면 이해가 편하다.\
이런 시맨틱 태그는 HTML5에서는 처음 등장했다. \
예를 들자면 헤더 또는  푸터같은 태그들을 말한다.\
이 태그들은 이름만 봐도 상단과 하단이라는 것을 쉽게  유추할수있다.\
이렇게 시맨틱 태그의 등장으로 인해 태그를 통해 좀더 쉽게 이해가 가능하다.

* `header`: 보통 사이트의 도입부에 표기된다. 머릿부분
* `hgroup`: 제목과 부제목을 묶어서 나타내어 주는 요소.
* `<section>` : 이름처럼 내용을 주제별로 나누거나 묶을 때 사용하는 태그이다.
* `<nav>` : 사이트의 네비게이션 탐색 메뉴를 나눌 때 사용되는 태그. 주로 `<li>`와 같이 사용된다.
* `<article>` : 독립적으로 출판될 수 있는 내용을 포함(예: 인스타 피드, 기사 내용, 대화형 위젯, 블로그 글, 제품 카드)
* `<header>, <footer>` : 보통 문서의 GNB(Global Navigation Bar)를 header의 자손으로 하고, 회사 정보 등을 footer에 넣는다.
* `<main>` : 문서의 핵심 주제나 핵심 기능과 관련있는 콘텐츠 작성. 한 페이지에 하나의 `<main>`태그가 올 수 있다.
* `<aside>` : 사이드바 또는 콜아웃 상자로 사용됨



* `<em>`: 텍스트의 강세(기울임). strong 태그와 유사하게 사용
* `<textarea>`: 두 줄 이상의 텍스트를 편집하는 박스
* `<datalist>`: 고를 수 있는 옵션들을 추천하는 선택지. option 요소를 여럿 담는다.
* `<option>`: select, optgroup, datalist 요소 안에 항목을 나타내는 옵션
* `<fieldset>`: 웹 양식의 여러 label을 묶을 때 사용한다. `<legend>` 요소로 그룹의 설명을 제공할 수도 잇다. -> 이전에 데모 프로젝트를 만들때 해당 시멘틱 태그때문에 곤혹스러웠던적이 있다...
*

## Inline Style

style" 속성을 활용한다. js 객체를 활용하여 변수, 함수를 재사용하기 좋다.

* inline style

```jsx
<div style={{ height: 10 }}>
  Hello World!
</div>
```

* style attribute

```jsx
const divStyle = {
  color: 'blue',
};

function App() {
  return <div style={divStyle}>Hello World!</div>;
}
```

### className 을 통해 적용하기

`index.html`

```html
<style>
 .greeting {
  color: #00F;
 }
</style>
```

`Greeting.jsx`

```jsx
export default function Greeting() {
 return (
  <p className="greeting">
   Hello, world!
  </p>
 );
}
```

공통된 부분이 많을 때 재사용하기 쉬움

그러나 css 는 컴포넌트를 전제로 하지 않기 때문에 컴포넌트 중심으로 작업하려고 하면 불편할 수 있다.\


가볍게 테스트할때는 인라인, 점차 살을 붙여나갈때는 className으로 재사용이 용이하도록 하자.

