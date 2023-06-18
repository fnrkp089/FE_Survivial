# ❗ AssignMent

## 재귀 함수 더 깊게 파기

```javascript
function deepCopy(obj) {
  let innerCopy;

  switch (true) {
    case Array.isArray(obj):
      innerCopy = obj.map((item) => deepCopy(item));
      break;
    case obj instanceof Date:
      innerCopy = new Date(obj);
      break;
    case obj instanceof Set:
      innerCopy = new Set([...obj].map((item) => deepCopy(item)));
      break;
    case obj instanceof Map:
      innerCopy = new Map([...obj].map(([key, value]) => [deepCopy(key), deepCopy(value)]));
      break;
    case typeof obj === 'object' && obj !== null:
      innerCopy = {};
      for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
          innerCopy[key] = deepCopy(obj[key]);
        }
      }
      break;
    default:
      return obj;
  }

  return innerCopy;
}
```

```javascript
case obj instanceof Set:
  innerCopy = new Set([...obj].map((item) => deepCopy(item)));
  break;
case obj instanceof Map:
  innerCopy = new Map([...obj].map(([key, value]) => [deepCopy(key), deepCopy(value)]));
  break;
```

* `case obj instanceof Set`: 해당 케이스는 입력으로 받은 `obj`가 `Set` 객체인지 확인합니다. `obj instanceof Set`은 `obj`가 `Set`의 인스턴스인지를 판별하는 조건문입니다.
* `innerCopy = new Set([...obj].map((item) => deepCopy(item)))`: `Set` 객체의 경우, `Set`의 내용물을 복사하기 위해 `Array.from()`이나 전개 연산자 `...`를 사용하여 `Set`을 배열로 변환합니다. 그리고 `map()` 메서드를 사용하여 배열의 각 요소에 대해 `deepCopy()` 함수를 호출하여 깊은 복사를 수행합니다. 마지막으로, `new Set()`을 사용하여 깊은 복사된 요소들로 이루어진 새로운 `Set` 객체를 생성합니다.
* `case obj instanceof Map`: 해당 케이스는 입력으로 받은 `obj`가 `Map` 객체인지 확인합니다. `obj instanceof Map`은 `obj`가 `Map`의 인스턴스인지를 판별하는 조건문입니다.
* `innerCopy = new Map([...obj].map(([key, value]) => [deepCopy(key), deepCopy(value)]))`: `Map` 객체의 경우, `Map`의 내용물을 복사하기 위해 `Array.from()`이나 전개 연산자 `...`를 사용하여 `Map`을 배열로 변환합니다. 그리고 `map()` 메서드를 사용하여 배열의 각 요소에 대해 `[key, value]` 배열을 생성하고, 그 안에서 `deepCopy()` 함수를 호출하여 키와 값 모두에 대해 깊은 복사를 수행합니다. 마지막으로, `new Map()`을 사용하여 깊은 복사된 키와 값으로 이루어진 새로운 `Map` 객체를 생성합니다.



정규 표현식(`RegExp`) 객체는 패턴(pattern)과 플래그(flags) 두 가지 중요한 속성을 가지고 있다:

1. 패턴(Pattern): 패턴은 정규 표현식에서 찾고자 하는 텍스트의 패턴을 정의한다.\
   &#x20;패턴은 일련의 문자열로 표현되며, 정규 표현식 엔진은 이 패턴을 사용하여 문자열에서 일치하는 부분을 찾는다. \
   패턴은 정규 표현식의 핵심이며, 다양한 메타 문자와 특수 문자를 사용하여 텍스트 패턴을 정확하게 지정할 수 있다.

ex) `/diablo/`은 "`diablo`"이라는 텍스트 패턴을 나타내는 정규 표현식입니다.

2. 플래그(Flags): 플래그는 정규 표현식의 동작을 조정하는 특수한 옵션을 나타낸다.\
   플래그는 패턴 뒤에 옵션으로 추가되며, 정규 표현식의 동작을 변경하거나 확장할 수 있다.&#x20;

> ex)
>
> * `i` (대소문자 구분 없음): 패턴 일치를 대소문자를 구분하지 않고 수행합니다.
> * `g` (전역 검색): 문자열 전체를 검색하여 패턴과 일치하는 모든 부분을 찾습니다.
> *   `m` (다중 행): 문자열이 여러 줄로 구성된 경우 각 줄의 시작과 끝을 고려하여 패턴과 일치하는 부분을 찾습니다.\
>
>
>     예를 들어, `/apple/gi`는 "apple"이라는 텍스트 패턴을 대소문자 구분 없이 전역 검색하도록 설정한 정규 표현식입니다.

정규 표현식(`RegExp`) 객체는 단순한 참조 복사로는 깊은 복사가 이루어지지 않습니다.\
정규 표현식 객체는 내부적으로 패턴(pattern)과 플래그(flags)라는 두 가지 속성을 가지고 있으며, 이러한 속성들은 변경 가능한 상태를 가질 수 있습니다. 따라서, 정확한 깊은 복사를 수행해야 합니다.



## 오브젝트를 만드는 방법들

1. **객체 리터럴 사용**: 일반적인 방법으로, 중괄호 `{}`를 사용하여 객체를 직접 정의합니다.

```javascript
javascriptCopy codelet obj = {
    key1: "value1",
    key2: "value2"
};
```

2. **Object 생성자 사용**: `new` 키워드와 `Object` 생성자를 사용하여 객체를 생성할 수 있습니다.

```javascript
javascriptCopy codelet obj = new Object();
obj.key1 = "value1";
obj.key2 = "value2";
```

3. **생성자 함수 사용**: 사용자 정의 생성자 함수를 사용하여 객체를 생성할 수도 있습니다. \
   생성자 함수는 일반적으로 대문자로 시작합니다.

```javascript
javascriptCopy codefunction MyObject(key1, key2) {
    this.key1 = key1;
    this.key2 = key2;
}
let obj = new MyObject("value1", "value2");
```

4. **Object.create() 메소드 사용**: 이 메소드는 명시적으로 프로토타입을 설정한 새 객체를 생성합니다.

```javascript
javascriptCopy codelet prototypeObject = {
    key1: "value1",
    key2: "value2"
};
let obj = Object.create(prototypeObject);
```

5. **ES6 클래스 사용**: ES6에서는 클래스 구문을 사용하여 객체를 생성할 수 있습니다.

```javascript
javascriptCopy codeclass MyObject {
    constructor(key1, key2) {
        this.key1 = key1;
        this.key2 = key2;
    }
}
let obj = new MyObject("value1", "value2");
```

1. **객체 리터럴 사용**: 이 방법은 단순하고 쉽게 사용할 수 있습니다. 즉석에서 객체를 생성하고 원하는 속성과 메서드를 추가할 수 있습니다. 그러나 이 방법은 빠르게 생성해야 하는 단일 객체에 대해 잘 작동하며, 유사한 객체를 여러 개 생성하려는 경우에는 적합하지 않습니다.
2. **Object 생성자 사용**: `new Object()`를 사용하여 객체를 생성하는 것은 객체 리터럴을 사용하는 것과 기본적으로 동일합니다. 그러나 이 방법은 코드가 좀 더 길어질 수 있습니다.
3. **생성자 함수 사용**: 생성자 함수는 사용자 정의 객체 타입을 만드는 데 유용합니다. 같은 타입의 여러 객체를 생성해야 하는 경우 특히 유용합니다. 그러나 이것은 초기 자바스크립트의 "클래스" 개념이므로, 이해하려면 자바스크립트의 `this`와 `new`에 대한 깊은 이해가 필요합니다.
4. **Object.create() 메소드 사용**: 이 메소드는 명시적으로 프로토타입을 설정하여 새 객체를 생성합니다. 이 방법은 프로토타입 기반 상속을 이용할 때 유용합니다. 그러나 `Object.create()`가 생성하는 모든 객체는 동일한 프로토타입을 공유하므로, 프로토타입에 대한 변경이 모든 객체에 영향을 미칠 수 있습니다.
5. **ES6 클래스 사용**: ES6 클래스는 사실상 문법적 설탕입니다 - 그것들은 생성자 함수를 더 쉽게 작성하고 읽을 수 있게 만드는 새로운 문법입니다. 클래스는 메서드, 생성자, 상속 등을 포함하여 객체 지향 프로그래밍을 보다 쉽게 구현할 수 있게 도와줍니다. 그러나 ES6 클래스를 이해하려면 `this`, `new`, 그리고 생성자 함수에 대한 이해가 여전히 필요합니다.
6. > 사람이 이해 하고 표현하기 쉽게 디자인된 프로그래밍 언어 문법. 또는 프로그래밍 언어를 더욱 더 간결하고 명확하게 표현이 가능하도록. 즉, sweeter하게 사용 할 수 있도록 도와주는 문법을 "Syntactic Sugar"라고 한다.

