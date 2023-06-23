# ❓ 질문내용

Q: Box Model에 대해 설명해주세요

A: 박스모델은 웹페이지의 요소들을 사각형의 형태로 보는것이며, 디자인과 레이아웃을 결정합니다.

1. **Content**: 이것은 요소의 실제 내용(텍스트, 이미지 등)을 포함합니다. 콘텐츠의 너비와 높이는 'width' 및 'height' 속성으로 제어할 수 있습니다.
2. **Padding**: 콘텐츠와 테두리 사이의 영역을 패딩이라 합니다. 이것은 상자 내부의 공간으로, 'padding' 속성으로 제어할 수 있습니다.
3. **Border**: 각 상자는 테두리를 가질 수 있습니다. 테두리는 'border' 속성으로 제어하며, 색상, 너비 및 스타일을 지정할 수 있습니다.
4. **Margin**: 마지막으로, 상자와 상자 사이의 공간을 마진이라 합니다. 이것은 상자 외부의 공간으로, 'margin' 속성으로 제어할 수 있습니다. 마진은 상자 간에 공간을 생성하며, 이는 특히 레이아웃에 중요한 역할을 합니다.

이 네 가지 요소는 모두 한 상자의 최종 크기를 결정합니다. 즉, 요소의 총 너비는 콘텐츠의 너비, 패딩, 테두리, 그리고 마진을 합한 값이 됩니다. 같은 방식으로 요소의 총 높이도 계산됩니다. 이는 CSS 레이아웃을 구성할 때 중요한 사항으로 고려되어야 합니다.

```
---------------------------------
|           Margin              |
|   -------------------------   |
|   |       Border           |  |
|   |   -------------------  |  |
|   |   |     Padding     |  |  |
|   |   |  -------------  |  |  |
|   |   |  |  Content  |  |  |  |
|   |   |  -------------  |  |  |
|   |   -------------------  |  |
|   -------------------------   |
---------------------------------

```

1. 중앙에 있는 "Content Box"는 웹 페이지에서 실제 내용(텍스트, 이미지 등)을 표시하는 부분입니다. 'width'와 'height' 속성은 이 영역의 크기를 결정합니다.
2. "Content Box"를 둘러싸는 다음 층은 "Padding Box"입니다. 이는 콘텐츠와 테두리(border) 사이의 공간을 제공합니다. 'padding' 속성을 사용하여 이 공간의 크기를 조절할 수 있습니다.
3. "Padding Box"를 둘러싸는 다음 층은 "Border Box"입니다. 이는 요소를 둘러싸는 테두리를 형성하며, 'border' 속성을 사용하여 테두리의 너비, 스타일, 색상을 설정할 수 있습니다.
4. 마지막으로, 가장 바깥층은 "Margin Box"입니다. 이는 요소와 그 주변 요소 사이의 공간을 형성하며, 'margin' 속성을 사용하여 이 공간의 크기를 조절할 수 있습니다.



Q:margin: 50px; padding: 20px; width: 300px; border: 5px; 위와 같을때 너비는 몇일까요? 즉 브라우저가 생각하는 전체 엘레멘트의 너비는 얼마일까요?

\
`box-sizing` 속성이 명시되지 않았으므로, 기본값인 `content-box`를 가정하겠습니다. 이 경우, 요소의 전체 너비는 다음과 같이 계산됩니다:

* Content의 너비 (`width`): 300px
* Padding: 양쪽에 각각 20px, 총 40px
* Border: 양쪽에 각각 5px, 총 10px
* Margin: 양쪽에 각각 50px, 총 100px

따라서 브라우저가 인식하는 전체 요소의 너비는 300px (content) + 40px (padding) + 10px (border) + 100px (margin) = 450px입니다.



Q: 어레이 안에서 순회시 출력이 안되는 요소는 뭐가 있을까요?

A: 어레이 안에서 "empty"라는 용어는 일반적으로 요소가 없거나 값이 비어있는 상태를 나타냅니다. 언어나 컨텍스트에 따라 "empty"라는 용어의 의미가 다를 수 있습니다.

어레이는 값의 순서화된 컬렉션으로, 일련의 요소를 포함할 수 있습니다. 때로는 어레이가 비어있는 경우, 즉 어떤 요소도 포함하지 않는 경우를 "empty array"라고 표현합니다. 이는 길이가 0인 어레이를 의미합니다.

예를 들어, JavaScript에서 빈 어레이를 생성하려면 다음과 같이 할 수 있습니다:

```javascript
const emptyArray = [];
console.log(emptyArray.length); // 0
```

따라서, "empty"라는 용어는 어레이 내부에 요소가 없는 상태를 나타내는 것을 의미합니다.



Q: 심볼이란 무엇인가요?

JavaScript에서 심볼(Symbol)은 원시 데이터 타입(Primitive Data Type) 중 하나로, \
ES6(ECMAScript 2015)에서 도입되었습니다. 심볼은 고유하고 변경 불가능한 값을 나타내며 주로 객체 속성의 식별자로 사용됩니다.

심볼은 다음과 같은 방법으로 생성됩니다:

```javascript
const mySymbol = Symbol();
```

심볼은 유일성을 보장하기 때문에 동일한 심볼 값을 가진 두 개의 심볼은 서로 다릅니다. 이를 통해 객체 속성을 식별하는 데 사용할 수 있습니다.

```javascript
const symbol1 = Symbol('description');
const symbol2 = Symbol('description');

console.log(symbol1 === symbol2); // false
```

심볼은 주로 객체 속성의 키로 사용되어 다른 속성과 충돌 없이 유일한 식별자로 활용됩니다. 심볼은 문자열과 마찬가지로 객체 속성에 사용될 수 있지만, 다른 속성들과는 분리되어 독립적으로 존재합니다.

```javascript
const mySymbol = Symbol('mySymbol');

const obj = {
  [mySymbol]: 'Hello, Symbol!'
};

console.log(obj[mySymbol]); // "Hello, Symbol!"
```

심볼은 일반적으로 내부적인 사용이나 고유한 식별자가 필요한 경우에 활용됩니다. 다른 데이터 타입과 달리 심볼은 외부에 노출되지 않고 비공개로 유지되기 때문에 보안적인 이점도 가지고 있습니다.



Q: 심볼을 만들어주세요

A:

```javascript
// Symbol생성
const mylittlesymbol =  Symbol(‘병관’);
console.log(typeof mylittlesymbol) //symbol?

//Symbol을 불러볼까요?
console.log(mylittlesymbol) //Symbol(‘병관’);

const mylittlesymbol2 = Symbol(‘병관’);

console.log(mylittlesymbol === mylittlesymbol2); //false

```

Q: 심볼을 만들려면 어떤 방법들이 있을까요?

A:

```javascript
// Create symbols
const sym1 = Symbol();
const sym2 = Symbol('foo');
const sym3 = Symbol('bar');

// Print symbols (use the description that was specified when calling Symbol function)
console.log(sym1);  // Symbol()
console.log(sym2);  // Symbol(foo)
console.log(sym3);  // Symbol(bar)

// Check type of symbol
console.log(typeof sym1);  // symbol
console.log(typeof sym2);  // symbol
console.log(typeof sym3);  // symbol
```

일반적으로 심볼은 객체의 프로퍼티 키로 사용됩니다.\
프로퍼티 키란 곧 해당 프로퍼티의 값에 접근하고자 할 때 사용하는 이름입니다.\
JavaScript에서 객체의 프로퍼티 키는 대개 문자열 값입니다.\
숫자로 쓰는 것도 사실은 문자열입니다.(내부적으로 문자열로 변환됨).

#### 내장 심볼 (Built-in Symbol)

Symbol 함수를 이용하여 직접 심볼을 생성하고 사용할 수도 있지만, 특별한 용도로 사용되기 위해 JavaScript 엔진 내에 미리 생성되어 상수로 존재하고 있는 내장 심볼(Built-in Symbol)들도 존재합니다.\
이들은 Symbol 함수의 프로퍼티로서 존재합니다\
자바스크립트가 기본 제공하는 빌트인 심벌값을 Well-known Symbols라고 부른다. 이는 자바스크립트 엔진의 내부 알고리즘에 사용된다.



Q: 가비지 컬렉션에 대해 말해주세요

A:자바스크립트에서 가비지 컬렉션은 메모리 관리 절차의 일부로서, 프로그래머가 명시적으로 메모리를 해제할 필요 없이 프로그램에서 더 이상 필요하지 않은 메모리를 자동으로 정리합니다. 이는 프로그래머가 실수로 메모리 누수를 일으키는 것을 방지하며, 메모리 관리를 크게 단순화합니다.

일반적으로 자바스크립트 개발자는 GC를 직접 조작하거나 제어하지 않고 자바스크립트 엔진이 자동으로 관리하도록 둡니다.&#x20;

> 1. **참조 표시(Mark-and-Sweep)**: 이 알고리즘은 'root' (즉, 전역 객체와 같은 루트 참조)에서 시작하여 참조할 수 있는 모든 객체를 '표시'합니다. 이 표시가 완료되면, 표시되지 않은 모든 객체는 메모리에서 제거되거나 'sweep' 됩니다. 이는 현재 가장 일반적으로 사용되는 가비지 컬렉션 알고리즘입니다.
> 2. **참조 카운팅(Reference Counting)**: 이 알고리즘은 객체에 대한 참조 수를 추적합니다. 참조 수가 0이되면 해당 객체는 더 이상 사용되지 않는 것으로 간주되며, 가비지 컬렉터에 의해 제거됩니다. 하지만, 이 방법은 순환 참조 문제를 야기할 수 있습니다. 즉, 서로 참조하는 두 객체가 다른 곳에서는 참조되지 않을 때, 두 객체 모두 참조 카운트가 0이 아니므로 가비지 컬렉터가 이들을 회수하지 못하게 됩니다.

가비지 컬렉션은 프로그램이 실행되는 동안 주기적으로 실행되며, 메모리 사용이 특정 임계값을 초과하면 강제로 실행될 수 있습니다. 가비지 컬렉션 프로세스는 필요한 CPU 시간을 소비하므로, 메모리를 효과적으로 관리하는 것은 웹 애플리케이션의 성능을 최적화하는 데 중요합니다.
