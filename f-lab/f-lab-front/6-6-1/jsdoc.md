# ❓ JSDoc

#### JSDoc란

Javasript 소스코드 파일에 주석을 달기위해 사용되는 마크업언어

주로 함수, 객체, 클래스, 변수 등의 요소에 대한 설명을 작성하는 데 사용된다.

&#x20;JSDoc 주석은 코드의 가독성과 이해를 돕고, 개발자들이 코드를 사용하고 유지보수할 때 도움이 되는 문서를 생성하는 데 도움을 준다고 한다.

JSDoc 주석은 다음과 같은 구조를 가진다.

```javascript
/**
 * @tag {type} name - description
 * ...
 */

```

* `@tag`: JSDoc 주석에서 사용되는 태그 예를 들어, `@param`, `@returns`, `@example` 등이 있다.\
  태그는 주석의 의미와 목적을 명확하게 표시하는 역할을 한다.
* `{type}`: 태그 뒤에 오는 값의 타입을 지정한다. \
  예를 들어, `{string}`, `{number}`, `{boolean}`, `{Array}`, `{Object}` 등과 같이 값을 타입으로 지정할 수 있다.
* `name`: 요소의 이름을 지정한다. 주로 함수의 매개변수, 반환값, 객체의 속성 등에 사용된다.
* `description`: 요소에 대한 설명을 작성한다. 주석 내에서 여러 줄로 작성할 수도 있다.

다음은 JSDocs로 만든 주석의 예이다

```javascript
/**
 * 이 함수는 두 수를 더합니다.
 * @param {number} a - 첫 번째 수
 * @param {number} b - 두 번째 수
 * @returns {number} - 두 수의 합
 */
function add(a, b) {
  return a + b;
}

```
