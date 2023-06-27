# ❤ Addtional Study

## 키와 값 할당

JavaScript에서 키와 값을 객체에 할당하는 방법은 여러 가지가 있습니다

1.  도트 표기법(Dot Notation):

    ```javascript
    const obj = {};
    obj.key = 'value';
    ```
2.  대괄호 표기법(Bracket Notation):

    ```javascript
    const obj = {};
    obj['key'] = 'value';
    ```
3.  객체 리터럴 내에서 키와 값을 할당:

    ```javascript
    const obj = {
      key: 'value'
    };
    ```
4.  Object.assign() 메서드 사용:

    ```javascript
    const obj = {};
    Object.assign(obj, { key: 'value' });
    ```
5.  ES6의 계산된 속성 이름(Computed Property Name)

    ```javascript
    const dynamicKey = 'age';

    const person = {
      name: 'lee',
      [dynamicKey]: 28
    };

    console.log(person); // { name: 'lee', age: 28}
    ```

    &#x20;`dynamicKey` 변수의 값을 사용하여 객체 `person`의 속성 이름을 동적으로 정의하고 있습니다. 이렇게 계산된 속성 이름을 사용하여 객체에 키와 값을 할당할 수 있습니다.
6.  객체 비구조화 할당(Object Destructuring Assignment)

    ```javascript
    const person = {
      name: 'lee',
      age: 28,
      address: {
        city: 'Seoul',
        country: 'Korea'
      }
    };

    const { name, age, address: { city } } = person;

    console.log(name); // 'lee'
    console.log(age); // 28
    console.log(city); // 'Seoul'
    ```

    위의 예시에서는 객체 `person`의 속성을 비구조화 할당하여 변수 `name`, `age`, `city`에 할당하고 있습니다. 이를 통해 객체의 속성을 추출하여 개별적인 변수로 사용할 수 있습니다. 객체 비구조화 할당은 객체의 중첩된 속성에도 적용할 수 있습니다.\




    1. 도트 표기법 (Dot Notation):
       * 차이점: 도트 표기법은 정적인 키를 사용하며, 키는 유효한 식별자여야 합니다.
       * 장점: 직관적이고 간결한 문법으로, 일반적인 경우에 사용하기 편리합니다.
    2. 대괄호 표기법 (Bracket Notation):
       * 차이점: 대괄호 표기법은 동적인 키를 사용할 수 있으며, 표현식을 사용하여 키를 작성할 수 있습니다.
       * 장점: 동적인 키를 사용할 수 있어 더 유연한 키 할당이 가능합니다.
    3. 객체 리터럴 내에서 키와 값을 할당:
       * 차이점: 객체 리터럴 내에서 키와 값을 할당하는 방법은 객체 생성 시 초기값을 지정할 때 사용됩니다.
       * 장점: 초기 객체 생성 시 편리하며, 여러 개의 키-값 쌍을 동시에 할당할 수 있습니다.
    4. Object.assign() 메서드 사용:
       * 차이점: Object.assign() 메서드를 사용하여 기존 객체를 변경하지 않고 새로운 객체를 생성하거나 여러 객체를 병합할 수 있습니다.
       * 장점: 기존 객체를 변경하지 않고 새로운 객체를 생성할 수 있으며, 여러 개의 소스 객체를 병합할 수 있습니다.
    5. ES6의 계산된 속성 이름 (Computed Property Name):
       * 차이점: 계산된 속성 이름을 사용하면 동적인 키를 생성할 수 있습니다. 표현식을 사용하여 키를 작성할 수 있습니다.
       * 장점: 동적인 키를 사용할 수 있어 더 유연한 키 할당이 가능합니다.
    6. ES6의 객체 비구조화 할당 (Object Destructuring Assignment):
       * 차이점: 객체 비구조화 할당은 객체의 특정 속성을 추출하여 변수에 할당하는 방법입니다.
       * 장점: 객체의 속성을 편리하게 추출하여 개별적인 변수로 사용할 수 있습니다. 중첩된 속성에도 적용할 수 있습니다.

    각 방법은 다양한 상황에서 활용될 수 있으며, 선택은 사용 환경과 요구 사항에 따라 달라집니다. 도트 표기법과 대괄호 표기법은 기본적인 키-값 할당에 사용되고, 객체 리터럴 내에서 키와 값을 할당하는 방법은 초기 객체 생성 시 사용됩니다. Object.assign() 메서드는 객체의 병합에 유용하며, 계산된 속성 이름과 객체 비구조화 할당은 동적인 상황에서 유연성을 제공합니다.

## DeepCopy

```javascript
function createRegExpCopy(obj) {
  return new RegExp(obj.source, obj.flags);
}

function createDateCopy(obj) {
  return new Date(obj.getTime());
}

function createSetCopy(obj) {
  return new Set();
}

function createMapCopy(obj) {
  return new Map();
}

function createArrayOrObjectCopy(obj) {
  if (Array.isArray(obj)) {
    return [];
  }
  return Object.create(Object.getPrototypeOf(obj));
}

function createCopy(obj, hash) {
  if (obj instanceof RegExp) {
    return createRegExpCopy(obj);
  }
  if (obj instanceof Date) {
    return createDateCopy(obj);
  }
  if (obj instanceof Set) {
    return createSetCopy(obj);
  }
  if (obj instanceof Map) {
    return createMapCopy(obj);
  }
  return createArrayOrObjectCopy(obj);
}

function deepCopy(obj, hash = new WeakMap()) {
  if (obj == null || typeof obj !== 'object') {
    return obj;
  }
  if (hash.has(obj)) {
    return hash.get(obj);
  }

  const clone = createCopy(obj, hash);

  hash.set(obj, clone);

  for (let key of Reflect.ownKeys(obj)) {
    clone[key] = deepCopy(obj[key], hash);
  }

  if (obj instanceof Set) {
    for (let value of obj) {
      clone.add(deepCopy(value, hash));
    }
  } else if (obj instanceof Map) {
    for (let [key, value] of obj) {
      clone.set(deepCopy(key, hash), deepCopy(value, hash));
    }
  }

  return clone;
}
```

\
`hash = new WeakMap()`은 순환 참조를 처리하기 위해 사용되는 객체입니다. WeakMap은 키-값 쌍을 저장하는데, 이 때 키는 약한 참조(weak reference)로 저장됩니다. 약한 참조는 가비지 컬렉션의 대상이 될 수 있는 참조로, 해당 객체에 다른 참조가 없는 경우 메모리에서 자동으로 해제될 수 있습니다.

`deepCopy` 함수에서 `hash`는 이미 방문한 객체를 기록하고 복사본을 저장하는 데 사용됩니다. 이를 통해 순환 참조가 있는 객체를 복사할 때 무한 재귀를 방지할 수 있습니다. 순환 참조가 발생한 객체는 이미 `hash`에 저장되어 있으므로, 해당 객체의 복사본을 반환하고 재귀적인 호출을 종료할 수 있습니다.

WeakMap을 사용하는 것은 순환 참조를 감지하고 처리하는 일반적인 방법 중 하나입니다. 이를 통해 깊은 복사 함수가 순환 참조를 올바르게 처리하고, 객체의 복사본을 정상적으로 생성할 수 있습니다.

### ex 1.)

```javascript
const obj1 = { name: 'John' };
const obj2 = { name: 'Alice' };

obj1.friend = obj2;  // obj1과 obj2가 서로를 참조하는 순환 참조 생성

const copy = deepCopy(obj1);
```

1. `obj1` 객체와 `obj2` 객체를 생성합니다.
2. `obj1` 객체의 `friend` 속성을 `obj2` 객체로 설정하여 순환 참조를 생성합니다.
3. `deepCopy(obj1)`을 호출하여 `obj1` 객체를 깊은 복사합니다.
4. `deepCopy` 함수 내부에서 `obj1`을 확인합니다.
5. `obj1`은 객체이므로 `typeof obj1 !== 'object'` 조건을 만족합니다.
6. `hash.has(obj1)`을 확인하여 `hash`에 `obj1`이 이미 존재하는지 확인합니다.
7. `hash`에 `obj1`이 없으므로 계속 진행합니다.
8. `createCopy(obj1, hash)`를 호출하여 `obj1`의 복사본을 생성합니다.
9. `createArrayOrObjectCopy(obj1)` 함수가 호출됩니다.
10. `obj1`은 일반 객체이므로 `Object.create(Object.getPrototypeOf(obj1))`을 통해 새로운 객체를 생성합니다.
11. `clone` 변수에 새로운 객체가 할당됩니다.
12. `hash.set(obj1, clone)`을 사용하여 `obj1`과 `clone`을 `hash`에 매핑합니다.
13. `Reflect.ownKeys(obj1)`을 사용하여 `obj1`의 프로퍼티를 순회합니다.
14. `key`가 `'name'`일 때, `obj1[key]`인 `'John'`을 복사하여 `clone[key]`에 할당합니다.
15. `key`가 `'friend'`일 때, `obj1[key]`인 `obj2`를 복사합니다.
16. `obj2`를 깊은 복사하기 위해 `deepCopy(obj2)`를 호출합니다.
17. `deepCopy` 함수 내부에서 `obj2`를 확인합니다.
18. `hash.has(obj2)`를 확인하여 `hash`에 `obj2`가 이미 존재하는지 확인합니다.
19. `hash`에 `obj2`가 없으므로 계속 진행합니다.
20. `createCopy(obj2, hash)`를 호출하여 `obj2`의 복사본을 생성합니다.
21. `createArrayOrObjectCopy(obj2)` 함수가 호출됩니다.
22. `obj2`는 일반 객체이므로 `Object.create(Object.getPrototypeOf(obj2))`을 통해 새로운 객체를 생성합니다.
23. `clone2` 변수에 새로운 객체가 할당됩니다.
24. `hash.set(obj2, clone2)`을 사용하여 `obj2`와 `clone2`를 `hash`에 매핑합니다.
25. `Reflect.ownKeys(obj2)`를 사용하여 `obj2`의 프로퍼티를 순회합니다. (여기서는 없음)
26. `clone2`를 `clone['friend']`에 할당합니다.
27. `clone` 객체가 최종적으로 반환됩니다.

### Ex2)

```javascript
const obj1 = { name: 'John' };
const obj2 = { name: 'Alice' };
const obj3 = { name: 'Bob' };

obj1.friend = obj2;  // obj1과 obj2 사이에 순환 참조 생성
obj2.friend = obj3;  // obj2와 obj3 사이에 순환 참조 생성
obj3.friend = obj1;  // obj3와 obj1 사이에 순환 참조 생성

const copy = deepCopy(obj1);
```

1. `obj1`, `obj2`, `obj3` 객체를 생성합니다.
2. `obj1` 객체의 `friend` 속성을 `obj2` 객체로 설정하여 `obj1`과 `obj2` 사이에 순환 참조를 생성합니다.
3. `obj2` 객체의 `friend` 속성을 `obj3` 객체로 설정하여 `obj2`와 `obj3` 사이에 순환 참조를 생성합니다.
4. `obj3` 객체의 `friend` 속성을 `obj1` 객체로 설정하여 `obj3`와 `obj1` 사이에 순환 참조를 생성합니다.
5. `deepCopy(obj1)`을 호출하여 `obj1` 객체를 깊은 복사합니다.

순환 참조는 다음과 같은 관계를 갖습니다:

* `obj1`의 `friend` 속성은 `obj2`를 참조하고 있습니다.
* `obj2`의 `friend` 속성은 `obj3`를 참조하고 있습니다.
* `obj3`의 `friend` 속성은 `obj1`을 참조하고 있습니다.

`deepCopy` 함수는 이러한 순환 참조를 정확하게 처리하면서 객체의 복사본을 생성합니다. 각 객체를 `hash`에 저장하여 이미 복사한 객체인지 확인하고, 순환 참조가 있을 경우 이전에 생성된 복사본을 반환하여 무한 재귀를 방지합니다. 따라서 `copy` 변수에는 `obj1`과 그 안의 객체들이 순환 참조를 피하고 복사된 복사본이 할당됩니다.

위의 예시에서 `WeakMap`은 순환 참조를 처리하기 위해 사용되는 객체입니다. `WeakMap`은 약한 참조(weak reference)를 사용하여 키-값 쌍을 저장하는 자료구조입니다. 약한 참조는 가비지 컬렉션의 대상이 될 수 있는 참조로, 해당 객체에 다른 강한 참조가 없는 경우 자동으로 메모리에서 해제될 수 있습니다.

`deepCopy` 함수에서 `hash` 변수는 `WeakMap` 객체로서 이미 방문한 객체와 해당 객체의 복사본을 저장하는 역할을 합니다. 이를 통해 순환 참조를 감지하고 처리할 수 있습니다. 아래는 `deepCopy` 함수를 호출할 때 `hash`를 이용하여 순환 참조를 처리하는 과정입니다:

1. `deepCopy(obj1)`을 호출하여 `obj1` 객체를 깊은 복사합니다.
2. `deepCopy` 함수 내부에서 `obj1`을 확인합니다.
3. `hash.has(obj1)`을 사용하여 `hash`에 `obj1`이 이미 존재하는지 확인합니다.
4. `hash`에 `obj1`이 없으므로 계속 진행합니다.
5. `createCopy(obj1, hash)`를 호출하여 `obj1`의 복사본을 생성합니다.
6. `createArrayOrObjectCopy(obj1)` 함수가 호출됩니다.
7. `obj1`은 일반 객체이므로 `Object.create(Object.getPrototypeOf(obj1))`을 통해 새로운 객체를 생성합니다.
8. `clone` 변수에 새로운 객체가 할당됩니다.
9. `hash.set(obj1, clone)`을 사용하여 `obj1`과 `clone`을 `hash`에 매핑합니다.
10. `Reflect.ownKeys(obj1)`을 사용하여 `obj1`의 프로퍼티를 순회합니다.
11. `key`가 `'name'`일 때, `obj1[key]`인 `'John'`을 복사하여 `clone[key]`에 할당합니다.
12. `key`가 `'friend'`일 때, `obj1[key]`인 `obj2` 객체를 복사합니다.
13. `deepCopy(obj2)`을 호출하여 `obj2` 객체를 깊은 복사합니다.
14. `deepCopy` 함수 내부에서 `obj2`를 확인합니다.
15. `hash.has(obj2)`를 사용하여 `hash`에 `obj2`가 이미 존재하는지 확인합니다.
16. `hash`에 `obj2`가 없으므로 계속 진행합니다.
17. `createCopy(obj2, hash)`를 호출하여 `obj2`의 복사본을 생성합니다.
18. `createArrayOrObjectCopy(obj2)` 함수가 호출됩니다.
19. `obj2`는 일반 객체이므로 `Object.create(Object.getPrototypeOf(obj2))`을 통해 새로운 객체를 생성합니다.
20. `clone2` 변수에 새로운 객체가 할당됩니다.
21. `hash.set(obj2, clone2)`을 사용하여 `obj2`와 `clone2`를 `hash`에 매핑합니다.

위의 과정을 통해 `WeakMap`인 `hash`를 사용하여 이미 방문한 객체를 저장하고, 순환 참조가 발생하더라도 이전에 생성한 복사본을 반환합니다. 이렇게 순환 참조를 처리하여 객체의 복사본을 올바르게 생성할 수 있습니다.

