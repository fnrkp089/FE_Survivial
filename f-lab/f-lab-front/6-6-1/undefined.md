---
description: additional study
---

# ❗ 추가 공부

* 객체 타입

1. `Object`: 속성과 메소드를 가지는 일반 객체. 예: `{}` 또는 `new Object()`
2. `Array`: 순서가 있는 항목들의 집합. 예: `[]` 또는 `new Array()`
3. `Function`: 실행 가능한 코드 블록을 나타내는 객체. 함수는 프로그램의 동작을 정의하고 재사용 가능한 코드 조각으로 사용
4. `Date`: 날짜와 시간 정보를 다루는 객체. 예: `new Date()`
5. `RegExp`: 정규표현식을 나타내는 객체. 문자열 패턴 매칭과 관련된 작업에 사용.

## Date / RegExp

1. `Date`: `Date` 객체는 날짜와 시간 정보를 다루는 객체이다. 날짜와 시간을 생성, 조작, 형식화하고, 날짜와 시간 간의 계산을 수행하는 데 사용된다. `Date` 객체는 `new Date()` 생성자를 사용하여 생성된다.

```javascript
const now = new Date();
console.log(now); // 예: Fri Jun 11 2023 10:30:00 GMT+0000 (Coordinated Universal Time)
```

2. `RegExp`: `RegExp` 객체는 정규표현식을 나타내는 객체이다. \
   정규표현식은 문자열 패턴 매칭과 관련된 작업을 수행하는 데 사용된다.\
   `RegExp` 객체는 정규표현식 리터럴 또는 `RegExp` 생성자를 사용하여 생성된다.

```javascript
const pattern = /abc/;
const regex = new RegExp('abc');
```

## 정규표현식

정규표현식(Regular Expression 또는 RegExp)은 텍스트에서 패턴을 검색하고 매칭하는 데 사용되는 도구라고 생각하면 편하다. \
문자열에 대한 검색, 대체, 분리, 추출 등의 작업을 수행할 때 유용하다.\
정규표현식은 패턴을 정의하고, 해당 패턴이 일치하는 문자열을 찾는 데 사용된다.

>
>
> 1. 문자열 매칭:
>    * `/hello/`: "hello"라는 문자열과 정확히 일치하는 패턴을 찾습니다.
>    * `/[A-Za-z]+/`: 알파벳 대소문자로 이루어진 단어를 찾습니다.
>    * `/\d+/`: 하나 이상의 숫자를 찾습니다.
> 2. 문자 클래스:
>    * `[abc]`: "a", "b", "c" 중 하나의 문자와 일치합니다.
>    * `[0-9]`: 0부터 9까지의 숫자 중 하나와 일치합니다.
>    * `[^0-9]`: 숫자가 아닌 문자와 일치합니다.
> 3. 반복:
>    * `a*`: "a"가 0회 이상 연속으로 나타나는 패턴과 일치합니다.
>    * `a+`: "a"가 1회 이상 연속으로 나타나는 패턴과 일치합니다.
>    * `a?`: "a"가 0 또는 1회 나타나는 패턴과 일치합니다.
> 4. 그룹화:
>    * `(abc)`: "abc"라는 그룹과 일치합니다. 매칭 결과에서 해당 그룹을 추출할 수 있습니다.
>    * `(red|blue)`: "red" 또는 "blue"와 일치하는 패턴을 찾습니다.
> 5. 시작과 끝:
>    * `/^hello/`: 문자열의 시작이 "hello"와 일치하는 패턴을 찾습니다.
>    * `/world$/`: 문자열의 끝이 "world"와 일치하는 패턴을 찾습니다.

`RegExp` 객체의 다양한 메소드(`test()`, `exec()`, `match()`, `replace()` 등)를 사용하여 정규표현식을 적용하고 작업을 수행할 수 있다.

## 복사

*   얕은 복사와 깊은복사

    * 얕은 복사(Shallow Copy):
      * 얕은 복사는 원본 객체의 속성들을 복사하여 새로운 객체를 생성한다.
      * 복사된 객체와 원본 객체는 같은 하위 객체를 참조한다. 즉, 하위 객체는 공유됨.
      * 하위 객체의 변경은 복사된 객체와 원본 객체 모두에 영향을 준다.
    *   깊은 복사(Deep Copy):

        * 깊은 복사는 원본 객체 및 하위 객체들을 재귀적으로 복사하여 모든 객체를 새로운 인스턴스로 생성한다..
        * 복사된 객체와 원본 객체는 서로 독립적인 객체이다. 하위 객체도 독립적으로 복사되므로, 변경이 서로에게 영향을 주지 않는다.



    ## 얕은 복사


* 전개 연산자

```
const originalArray = [1, 2, 3, 4, 5];
const copiedArray = [...originalArray];

const originalObject = { name: "John", age: 25 };
const copiedObject = { ...originalObject };
```

* Object.assign():

```
const originalObject = { name: "John", age: 25 };
const copiedObject = Object.assign({}, originalObject);
```

전개 연산자(`...`)와 `Object.assign()` 메서드는 모두 자바스크립트에서 객체나 배열의 얕은 복사를 수행.

Object.assign은 첫 번째 인자로 들어간 객체를 조작하고, spread operator는 새 객체를 반환한다고 하는데,\
Object.assign(a,  etc...) 하면 a 자체가 변한다.  즉a 변수 자체에 조작을 가하게 된다.

하지만 { ...a,  etc} 를 하게되면 a 와 etc가합쳐진 새로운 객체를 만든다. \
a 자체는 여전히 원래의 값을 유지한 다는 것!

## 깊은 복사



*   JSON.stringify()와 JSON.parse()을 사용한 복사와, 재귀복사의 차이점:

    * **`JSON.stringify()`** 및 **`JSON.parse()`** 방법은 객체를 문자열로 변환하고 다시 객체로 역직렬화하여 복사한다. 이 과정에서 데이터의 특수한 유형이 유실될 수 있다.
      1. 함수:
         * JavaScript의 함수는 실행 가능한 코드이므로 JSON으로 직렬화할 수 없다.
         * \*\*`JSON.stringify()`\*\*를 사용하여 객체를 문자열로 변환할 때, 함수는 무시되거나 \*\*`null`\*\*로 변환된다.
         * \*\*`JSON.parse()`\*\*를 사용하여 문자열을 객체로 역직렬화할 때, 함수는 일반 객체로 변환되며, 실행 가능한 함수로 복원되지 않는다.
      2. 정규표현식:
         * 정규표현식 객체도 JSON으로 직렬화할 수 없다.
         * \*\*`JSON.stringify()`\*\*를 사용하여 객체를 문자열로 변환할 때, 정규표현식은 무시되거나 \*\*`{}`\*\*와 같은 빈 객체로 변환된다.
         * \*\*`JSON.parse()`\*\*를 사용하여 문자열을 객체로 역직렬화할 때, 정규표현식은 일반 객체로 변환되며, 정규표현식 기능을 잃는다.
    * 재귀적 복사는 객체의 모든 속성을 개별적으로 탐색하면서 새로운 객체를 생성한다. 이 방법은 객체의 속성 값이 함수나 정규표현식과 같은 특수한 유형의 데이터도 완벽하게 복사한다.

    따라서, 재귀적 복사를 사용하면 더 완전한 복사를 수행할 수 있고, 데이터의 일관성과 무결성을 보장할수 있다고 한다. 그러나 재귀적 복사 방법은 구현이 복잡하고, 성능 문제가 발생할 수 있다.



## JSON.stringify()와 JSON.parse()?

\
`JSON.stringify()`와 `JSON.parse()`는 JavaScript에서 JSON 데이터를 처리하는 데 사용되는 메소드이다.

>
>
> 1. `JSON.stringify()`:
>    * `JSON.stringify()` 메소드는 JavaScript 객체나 값의 JSON 문자열 표현을 생성합니다.
>    * 원본 객체를 JSON 형식의 문자열로 직렬화(serialize)합니다.
>    * 객체의 속성들을 문자열로 변환하고, 이들을 JSON 형식으로 조합하여 문자열을 생성합니다.
>    * JSON.stringify(value\[, replacer\[, space]]) 형식으로 사용됩니다.
>    * `value`: JSON 문자열로 변환할 JavaScript 객체나 값입니다.
>    * `replacer` (옵션): 문자열 또는 함수로, 특정 속성을 포함하거나 필터링하여 직렬화에 사용됩니다.
>    * `space` (옵션): 들여쓰기를 위한 공백 문자열 또는 공백 개수를 나타내는 숫자입니다.
> 2. `JSON.parse()`:
>    * `JSON.parse()` 메소드는 JSON 문자열을 JavaScript 객체로 역직렬화(deserialize)합니다.
>    * JSON 형식의 문자열을 JavaScript 객체로 변환합니다.
>    * JSON.parse(text\[, reviver]) 형식으로 사용됩니다.
>    * `text`: JSON 문자열로 변환할 JavaScript 객체나 값입니다.
>    * `reviver` (옵션): 함수로, 역직렬화 중에 값 변환을 위해 호출됩니다.

```javascript
const person = {
  name: 'LeeByeongKwan',
  age: 28,
  hobbies: ['reading', 'running']
};

const jsonString = JSON.stringify(person);
console.log(jsonString);
// 출력: {"name":"LeeByeongKwan","age":28,"hobbies":["reading","running"]}

const parsedObject = JSON.parse(jsonString);
console.log(parsedObject);
// 출력: { name: 'LeeByeongKwan', age: 28, hobbies: [ 'reading', 'running' ] }


```



## 재귀적으로 깊은 복사 수행하기.

```javascript
/**
 * 주어진 객체를 깊은 복사하여 반환합니다.
 *
 * @param {Array|Object} obj - 복사할 객체 또는 배열.
 * @returns {Array|Object} - 깊은 복사된 새로운 객체 또는 배열.
 */
function deepCopy(obj) {
  let innerCopy;

  if (Array.isArray(obj)) {
    innerCopy= [];
  } else if (typeof obj === 'object' && obj !== null) {
    innerCopy= {};
  } else {
    return obj;
  }

  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepCopy(obj[key]);
    }
  }

  return copy;
}

```

재귀적으로 호출되는 과정

예시로 다음과 같은 중첩된 객체를 깊은 복사하는 경우를 가정하자:

```javascript
const originalObj = {
  name: 'LeeByeongKwan',
  age: 28,
  address: {
    city: 'Seoul',
    country: 'Korea'
  }
};

```

1. 최초 호출:
   * `deepCopy(originalObj)` 함수가 최초로 호출됩니다.
   * `obj` 매개변수에는 `originalObj`가 전달됩니다.
   * 새로운 빈 객체 `copy`가 생성됩니다.
2. 첫 번째 속성 복사:
   * `for...in` 루프에서 첫 번째 속성 `'name'`에 대해 순회합니다.
   * `key` 변수에는 `'name'`이 할당됩니다.
   * `obj[key]`는 `'LeeByeongKwan'`을 반환합니다.
   * `deepCopy('LeeByeongKwan')`이 재귀적으로 호출됩니다.
   * `'LeeByeongKwan'`은 원시 값이므로 복사하지 않고 그대로 반환됩니다.
   * `copy['name']`에는 `'LeeByeongKwan'`이 할당됩니다.
3. 두 번째 속성 복사:
   * `for...in` 루프에서 두 번째 속성 `'age'`에 대해 순회합니다.
   * `key` 변수에는 `'age'`가 할당됩니다.
   * `obj[key]`는 `28`을 반환합니다.
   * `deepCopy(28)`이 재귀적으로 호출됩니다.
   * `28`은 원시 값이므로 복사하지 않고 그대로 반환됩니다.
   * `copy['age']`에는 `28`이 할당됩니다.
4. 세 번째 속성 복사:
   * `for...in` 루프에서 세 번째 속성 `'address'`에 대해 순회합니다.
   * `key` 변수에는 `'address'`가 할당됩니다.
   * `obj[key]`는 내부 객체 `{ city: 'Seoul', country: 'Korea' }`를 반환합니다.
   * `deepCopy({ city: 'Seoul', country: 'Korea' })`가 재귀적으로 호출됩니다.
5. 내부 객체 복사:
   * `deepCopy({ city: 'Seoul', country: 'Korea' })`에서 새로운 빈 객체 `innerCopy`가 생성됩니다.
6. 내부 객체의 속성 복사:
   * `for...in` 루프에서 `'city'` 속성에 대해 순회합니다.
   * `key` 변수에는 `'city'`가 할당됩니다.
   * `obj[key]`는 `'Seoul'`을 반환합니다.
   * `deepCopy('Seoul')`이 재귀적으로 호출됩니다.
   * `'Seoul'`은 원시 값이므로 복사하지 않고 그대로 반환됩니다.
   * `innerCopy['city']`에는 `'Seoul'`이 할당됩니다.
7. 내부 객체의 속성 복사:
   * `for...in` 루프에서 `'country'` 속성에 대해 순회합니다.
   * `key` 변수에는 `'country'`가 할당됩니다.
   * `obj[key]`는 `'Korea'`를 반환합니다.
   * `deepCopy('Korea')`가 재귀적으로 호출됩니다.
   * `'Korea'`는 원시 값이므로 복사하지 않고 그대로 반환됩니다.
   * `innerCopy['country']`에는 `'Korea'`이 할당됩니다.
8. 내부 객체 복사 완료:
   * `innerCopy` 객체가 완성되었습니다.
9. 내부 객체 복사본 할당:
   * `copy['address']`에 `innerCopy` 객체가 할당됩니다.
10. 재귀 호출 결과 반환:
    * `copy` 객체가 완성되었습니다.
11. 최종 결과 반환:
    * `copy` 객체가 최종 결과로 반환됩니다.
