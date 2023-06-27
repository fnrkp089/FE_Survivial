# ❤ Addtional Study

## 키와 값 할당

1.  **객체 리터럴 사용하기**:

    ```javascript
    let obj = {
        key1: 'value1',
        key2: 'value2',
        key3: 'value3'
    };
    ```

    위 코드에서 `obj`는 `key1`, `key2`, `key3`라는 키를 가지고 각각의 키에 대한 값으로 `'value1'`, `'value2'`, `'value3'`를 가지는 객체를 생성합니다.\

2.  **대괄호(`[]`) 또는 점(`.`) 표기법 사용하기**:

    ```javascript
    let obj = {};
    obj['key1'] = 'value1';
    obj.key2 = 'value2';
    ```

    `obj`는 빈 객체를 먼저 생성하고, 그 후에 키와 값을 추가하는 코드입니다. 대괄호(`[]`) 또는 점(`.`) 표기법을 사용하여 키를 지정하고 값을 할당할 수 있습니다. 이 방법은 동적으로 키를 생성하거나 기존 객체에 새로운 키-값 쌍을 추가할 때 유용합니다.\

3.  **Object.assign 메서드 사용하기**:

    ```javascript
    let obj = Object.assign({}, {key1: 'value1', key2: 'value2'});
    ```

    `Object.assign` 메서드는 대상 객체에 하나 이상의 출처 객체로부터 모든 열거 가능한 자체 속성을 복사하여 대상 객체에 적용합니다. 이 방법은 여러 출처 객체들의 속성들을 하나의 대상 객체로 병합할 때 유용합니다.\

4.  **ES6의 스프레드 연산자(`...`) 사용하기**:

    ```javascript
    let obj = {...{key1: 'value1', key2: 'value2'}};
    ```

    스프레드 연산자(`...`)는 ES6에 도입된 기능으로, 객체의 모든 키-값 쌍을 새 객체에 복사합니다. 이 방법은 기존 객체를 복사하거나 기존 객체에 새로운 속성을 추가하여 새로운 객체를 생성할 때 유용합니다.\

5.  **ES6의 Map 객체 사용하기**:

    ```javascript
    jlet map = new Map();
    map.set('key1', 'value1');
    map.set('key2', 'value2');
    ```

    `Map`은 ES6에서 추가된 데이터 구조로, 키-값 쌍을 저장합니다. `Map`은 일반 객체와 달리 어떤 값도 키로 사용할 수 있으며, 키-값 쌍의 삽입 순서를 기억합니다

### 각각의 차이점&#x20;

1. **객체 리터럴 사용하기**: 객체 리터럴을 사용하여 키와 값을 한 번에 할당하는 것은 편리하며, 코드가 간결해집니다. 하지만, 이 방법은 키 이름이 사전에 알려져 있어야 하며, 키 이름을 동적으로 생성할 수 없습니다.
2. **대괄호(`[]`) 또는 점(`.`) 표기법 사용하기**: 이 방법을 사용하면 키 이름을 동적으로 생성할 수 있습니다. 즉, 키 이름이 변수에 저장된 경우 또는 실행 시간에 키 이름을 결정해야 하는 경우에 유용합니다. 대괄호(`[]`) 표기법을 사용하면 변수나 표현식을 키 이름으로 사용할 수 있지만, 점(`.`) 표기법을 사용하면 문자열 리터럴만 키 이름으로 사용할 수 있습니다.
3. **Object.assign 메서드 사용하기**: `Object.assign` 메서드는 여러 출처 객체들의 속성들을 하나의 대상 객체로 병합하는 데 유용합니다. 그러나 이 방법은 깊은 복사(deep copy)를 수행하지 않으므로, 출처 객체의 속성 값이 객체인 경우 대상 객체에서 해당 속성을 변경하면 원본 객체도 변경됩니다.
4. **ES6의 스프레드 연산자(`...`) 사용하기**: 스프레드 연산자(`...`)도 `Object.assign`과 마찬가지로 여러 출처 객체들의 속성들을 하나의 대상 객체로 병합하는 데 사용됩니다. 하지만 스프레드 연산자(`...`)는 `Object.assign`과는 다르게 배열과 같은 이터러블(iterable) 객체에서도 사용할 수 있습니다.
5. **ES6의 Map 객체 사용하기**: `Map` 객체는 일반 객체와는 다르게 어떤 값도 키로 사용할 수 있습니다. 또한, 키-값 쌍의 삽입 순서를 유지하며, `Map` 객체에 저장된 요소의 개수를 쉽게 알아낼 수 있습니다(`Map.prototype.size` 속성을 통해). 그러나 `Map` 객체는 일반 객체보다 다루기가 조금 더 복잡하며, 키-값 쌍을 저장하고 검색하는 방법도 일반 객체와는 다릅니다(`Map.prototype.set`, `Map.prototype.get` 메서드를 사용).

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

