# 🗺 Map vs WeakMap

## Map

`Map`은 JavaScript에서 제공하는 내장 객체로, 키-값 쌍을 저장하는 데 사용됩니다. \
배열과 유사하지만, 배열과 달리 Map은 키의 타입에 제한이 없으며 \
(즉, 객체, 함수, NaN 등 모든 타입의 키), \
순서가 보장되며, 키-값 쌍에 대한 효율적인 삽입, 검색, 삭제를 위한 메서드를 제공합니다.

`Map` 객체의 주요 메서드와  속성은 다음과 같습니다.

1. **new Map(\[iterable])**: 새로운 Map 객체를 생성합니다. 선택적으로 iterable (예: 배열의 배열)을 전달하여 키-값 쌍을 초기화할 수 있습니다.
2. **map.set(key, value)**: Map에 키-값 쌍을 설정합니다. 키가 이미 Map에 존재하는 경우, 해당 키의 값을 업데이트합니다. 새로운 키라면 키-값 쌍을 추가합니다.
3. **map.get(key)**: 주어진 키에 대한 값을 반환합니다. 키가 Map에 없는 경우 `undefined`를 반환합니다.
4. **map.has(key)**: 주어진 키가 Map에 존재하면 `true`를, 그렇지 않으면 `false`를 반환합니다.
5. **map.delete(key)**: 주어진 키의 키-값 쌍을 Map에서 삭제하고, 삭제에 성공하면 `true`를, 그렇지 않으면 `false`를 반환합니다.
6. **map.clear()**: Map의 모든 키-값 쌍을 삭제합니다.
7. **map.size**: Map에 있는 키-값 쌍의 개수를 반환합니다.
8. **map.keys()**: Map의 모든 키를 반환하는 새로운 Iterator 객체를 반환합니다.
9. **map.values()**: Map의 모든 값을 반환하는 새로운 Iterator 객체를 반환합니다.
10. **map.entries()**: Map의 모든 키-값 쌍을 반환하는 새로운 Iterator 객체를 반환합니다. 이 메서드는 `Map` 객체가 기본적으로 iterable이므로 `for...of` 루프에서 Map을 직접 반복할 때도 사용됩니다.

```javascript
javascriptCopy codelet map = new Map();

// Setting key-value pairs
map.set('name', 'lee');
map.set('age', 25);

// Getting the values
console.log(map.get('name')); // Output: lee
console.log(map.get('age'));  // Output: 25

// Checking if a key exists
console.log(map.has('name')); // Output: true
console.log(map.has('job'));  // Output: false

// Checking the size
console.log(map.size); // Output: 2

// Deleting a key-value pair
map.delete('age');
console.log(map.has('age')); // Output: false
console.log(map.size); // Output: 1

// Clearing the map
map.clear();
console.log(map.size); // Output: 0
```

Map은 다음과 같은 상황에서 유용할 수 있습니다.

1. 데이터 관리: `Map`은 키-값 쌍을 사용하여 데이터를 구조화하고 관리하는 데 유용합니다. 예를 들어, 객체나 배열 대신 `Map`을 사용하여 데이터를 저장하면 키를 통해 쉽게 값을 찾을 수 있습니다.
2. 중복 키 관리: `Map`은 중복된 키를 허용하므로, 중복 키를 가진 데이터를 저장하고 조회하는 데 사용할 수 있습니다. 예를 들어, `Map`을 사용하여 단어의 등장 횟수를 세거나, 학생의 성적을 저장할 수 있습니다.
3. 순서 보장: `Map`은 요소의 삽입 순서를 보장하므로, 데이터를 순차적으로 처리하거나 순회해야 할 때 유용합니다. 이를 통해 데이터의 순서를 유지하고 처리 과정을 예측 가능하게 만들 수 있습니다.
4. 객체 대체: `Map`은 객체보다 유연한 키 타입을 허용하므로, 특정 객체를 키로 사용해야 하는 경우에 유용합니다. 객체는 문자열로 변환되어 키로 사용될 때 일부 정보가 손실될 수 있지만, `Map`은 원래의 키를 그대로 유지합니다.



> Ex)
>
>
>
> 1.  학생 성적표 관리: 학생의 이름을 키로 사용하고, 성적을 값으로 사용하여 `Map`을 생성하여 학생들의 성적표를 관리할 수 있습니다. 이렇게 하면 학생 이름을 키로 사용하여 성적을 쉽게 조회하거나 업데이트할 수 있습니다.
>
>     ```javascript
>     const studentGrades = new Map();
>
>     studentGrades.set('lee', 1);
>     studentGrades.set('byeong', 2);
>     studentGrades.set('kwan', 3);
>
>     console.log(studentGrades.get('lee')); // 1
>     ```
> 2.  이벤트 핸들러 관리: 이벤트 이름을 키로 사용하고, 해당 이벤트에 연결된 핸들러 함수를 값으로 사용하여 `Map`을 생성하여 이벤트 핸들러를 관리할 수 있습니다. 이렇게 하면 특정 이벤트에 대한 핸들러를 쉽게 추가하거나 제거할 수 있습니다.
>
>     ```javascript
>     const eventHandlers = new Map();
>
>     function handleButtonClick() {
>       console.log('Button clicked!');
>     }
>
>     eventHandlers.set('click', handleButtonClick);
>
>     // 이벤트가 발생하면 해당 핸들러를 호출합니다.
>     const eventType = 'click';
>     if (eventHandlers.has(eventType)) {
>       const eventHandler = eventHandlers.get(eventType);
>       eventHandler();
>     }
>     ```
> 3.  데이터 순회: `Map`은 요소의 삽입 순서를 보장하므로, 데이터를 순차적으로 처리해야 할 때 유용합니다. 예를 들어, `Map`에 저장된 항목들을 반복문으로 순회하여 처리할 수 있습니다.
>
>     ```javascript
>     const userRoles = new Map();
>
>     userRoles.set('lee', 'warlock');
>     userRoles.set('byeong', 'titan');
>     userRoles.set('kwan', 'hunter');
>
>     // 사용자 역할을 출력합니다.
>     for (const [user, role] of userRoles) {
>       console.log(`${user}의 역할: ${role}`);
>     }
>     ```



## WeakMap

`WeakMap`은 JavaScript에서 제공하는 특별한 종류의 Map입니다. 일반 `Map`과의 주요 차이점은 키가 반드시 객체여야 하며, 키에 대한 참조가 약하다는 것입니다. 이는 가비지 컬렉션(GC) 시스템에 의해 키가 자동으로 제거될 수 있다는 의미입니다. 즉, `WeakMap`에 키로 사용된 객체에 대한 다른 참조가 없다면, 그 키-값 쌍은 언제든 가비지 컬렉터에 의해 메모리에서 해제될 수 있습니다.

`WeakMap` 객체의 주요 메서드와  속성은 다음과 같습니다.

1. **new WeakMap(\[iterable])**: 새로운 WeakMap 객체를 생성합니다. 선택적으로 iterable (예: 배열의 배열)을 전달하여 키-값 쌍을 초기화할 수 있습니다.
2. **weakMap.set(key, value)**: WeakMap에 키-값 쌍을 설정합니다. 키가 이미 WeakMap에 존재하는 경우, 해당 키의 값을 업데이트합니다. 새로운 키라면 키-값 쌍을 추가합니다. 키는 반드시 객체여야 합니다.
3. **weakMap.get(key)**: 주어진 키에 대한 값을 반환합니다. 키가 WeakMap에 없는 경우 `undefined`를 반환합니다.
4. **weakMap.has(key)**: 주어진 키가 WeakMap에 존재하면 `true`를, 그렇지 않으면 `false`를 반환합니다.
5. **weakMap.delete(key)**: 주어진 키의 키-값 쌍을 WeakMap에서 삭제하고, 삭제에 성공하면 `true`를, 그렇지 않으면 `false`를 반환합니다.

```javascript
javascriptCopy codelet weakMap = new WeakMap();

let obj1 = {};
let obj2 = {};

// Setting key-value pairs
weakMap.set(obj1, 'lee');
weakMap.set(obj2, 25);

// Getting the values
console.log(weakMap.get(obj1)); // Output: lee
console.log(weakMap.get(obj2));  // Output: 25

// Checking if a key exists
console.log(weakMap.has(obj1)); // Output: true
console.log(weakMap.has({}));  // Output: false

// Deleting a key-value pair
weakMap.delete(obj2);
console.log(weakMap.has(obj2)); // Output: false
```

`WeakMap`은 주로 객체에 연관된 private 데이터를 저장하는 데 사용됩니다. \
그리고 객체가 가비지 컬렉트 될 때 자동으로 그 연관 데이터가 삭제되는 것을 보장합니다. 이는 메모리 관리 측면에서 유용합니다.

## Map? WeakMap?

`Map`과 `WeakMap`은 JavaScript에서 제공하는 두 가지 유형의 컬렉션 객체입니다. 그런데 이 둘은 동작 방식과 특성에서 몇 가지 중요한 차이점을 가지고 있습니다.

**Map**:

* Map은 키-값 쌍을 저장합니다.
* Map에서 키는 임의의 값(객체, 원시 값 등)이 될 수 있습니다.
* Map의 키-값 쌍은 삽입 순서를 유지하므로 순회 가능합니다.
* Map에는 `.size`라는 속성이 있어 Map에 있는 요소의 수를 쉽게 확인할 수 있습니다.
* Map은 `clear()` 메서드를 사용하여 모든 요소를 한 번에 제거할 수 있습니다.

**WeakMap**:

* WeakMap도 키-값 쌍을 저장합니다.
* WeakMap의 키는 오직 객체만 될 수 있습니다. 원시 값은 키로 사용될 수 없습니다.
* WeakMap은 키에 대한 참조를 약하게(weakly) 유지합니다. 이는 키에 대한 참조가 가비지 컬렉션의 대상이 될 수 있음을 의미합니다. 즉, WeakMap의 키 객체에 대한 다른 참조가 없다면 가비지 컬렉터는 그 키-값 쌍을 메모리에서 해제할 수 있습니다.
* WeakMap은 순회할 수 없으며, `.size` 속성도 없습니다. 이는 가비지 컬렉터에 의해 언제든지 키-값 쌍이 제거될 수 있기 때문입니다.
* WeakMap에는 `clear()` 메서드가 없습니다.

**차이점**:

* Map은 어떤 종류의 키도 허용하는 반면, WeakMap은 오직 객체만 키로 허용합니다.
* Map은 순회 가능하지만, WeakMap은 순회할 수 없습니다.
* WeakMap의 키-값 쌍은 가비지 컬렉션의 대상이 될 수 있지만, Map은 그렇지 않습니다.
* Map은 `.size` 속성과 `clear()` 메서드를 제공하는 반면, WeakMap은 제공하지 않습니다.

일반적으로, 각 객체는 사용 사례에 따라 선택되어야 합니다. 객체에 연결된 private 데이터를 저장할 때 WeakMap이 유용하며, 키-값 쌍의 컬렉션을 순회하거나 관리해야 할 때는 Map이 더 적합합니다.

> JavaScript의 `Map` 객체에서 `.size` 속성과 `clear()` 메서드는 다음과 같은 역할을 합니다.
>
> **.size 속성**:
>
> * `Map` 객체의 `.size` 속성은 Map에 있는 요소의 수를 반환합니다.
> * 예를 들어, 만약 Map에 키-값 쌍이 3개 있다면, `map.size`는 3을 반환할 것입니다.
>
> ```javascript
> javascriptCopy codelet map = new Map();
> map.set('a', 1);
> map.set('b', 2);
> map.set('c', 3);
>
> console.log(map.size); // 출력: 3
> ```
>
> **clear() 메서드**:
>
> * `Map` 객체의 `clear()` 메서드는 Map에서 모든 요소를 제거합니다.
> * `clear()` 메서드는 아무런 매개변수를 받지 않으며, 호출한 Map을 비우고 아무것도 반환하지 않습니다.
>
> ```javascript
> javascriptCopy codelet map = new Map();
> map.set('a', 1);
> map.set('b', 2);
> map.set('c', 3);
>
> console.log(map.size); // 출력: 3
>
> map.clear();
>
> console.log(map.size); // 출력: 0
> ```
>
> 위의 코드에서는 `map.clear()`를 호출하여 Map의 모든 요소를 제거한 후, `map.size`를 호출하여 Map이 비어있음을 확인합니다.



## WeakMap의 약한 참조

**`WeakMap`의 약한 참조(weak reference) 특성은 주로 메모리 관리 및 객체 생명주기와 관련이 있습니다**.

일반적인 `Map`에서 키-값 쌍을 생성하면, Map은 키에 대한 강한 참조(strong reference)를 유지합니다. **즉, 키로 사용된 객체가 메모리에서 제거되려면 명시적으로 Map에서 해당 키를 삭제해야 합니다.** 그렇지 않으면 메모리 누수가 발생할 수 있습니다.

> 좀 더 명확히 설명하자면, JavaScript의 가비지 컬렉터는 객체가 더 이상 사용되지 않을 때 해당 객체를 메모리에서 제거합니다. "사용되지 않는다"는 의미는 해당 객체에 대한 참조가 더 이상 존재하지 않는 상황을 말합니다.\
>

반면에 `WeakMap`에서는 키에 대한 약한 참조를 유지합니다. 이는 `WeakMap`에 저장된 키-값 쌍이 키 객체에 대한 유일한 참조가 되지 않도록 보장합니다. 다시 말해, 키 객체에 대한 모든 다른 참조가 사라지면, 가비지 컬렉터는 그 키-값 쌍을 메모리에서 자동으로 해제할 수 있습니다.\


> 만약 어떤 객체를 Map의 키로 사용했다면, 해당 Map은 그 객체에 대한 참조를 가지고 있게 됩니다. 따라서 해당 객체는 "사용되고 있는" 상태로 간주되므로 가비지 컬렉션의 대상이 되지 않습니다. 그 객체를 메모리에서 해제하려면 Map에서 해당 키-값 쌍을 명시적으로 삭제해야 하며, 그 이후에 객체에 대한 다른 참조가 없다면 가비지 컬렉터가 그 객체를 메모리에서 제거할 수 있습니다.
>
> 이러한 동작은 메모리 누수를 발생시킬 수 있는 위험을 내포하고 있습니다. 예를 들어, 큰 데이터를 가진 객체를 키로 사용하고, 그 객체를 다른 곳에서는 더 이상 참조하지 않더라도, Map에서 그 키-값 쌍을 삭제하지 않는 한 해당 객체는 계속 메모리에 남아있게 됩니다.
>
> 반면, WeakMap에서는 키에 대한 참조가 "약한 참조"입니다. 이는 WeakMap이 키 객체에 대한 참조를 유지하지만, 그 참조가 가비지 컬렉션을 방해하지 않는다는 의미입니다. 따라서 WeakMap에 키로 사용된 객체에 대한 다른 참조가 없다면, 가비지 컬렉터는 그 키-값 쌍을 메모리에서 자동으로 제거할 수 있습니다. 이로 인해 메모리 관리가 더욱 용이해집니다.

따라서 `WeakMap`은 객체에 연결된 private 데이터를 저장하는 경우에 유용합니다. 해당 객체가 더 이상 필요하지 않으면 자동으로 그에 연결된 데이터도 메모리에서 제거되므로, 개발자가 메모리 관리에 신경 쓸 필요가 줄어듭니다.

또한, `WeakMap`의 이러한 특성은 객체가 가비지 컬렉션의 대상이 될 수 있는지 결정하는 데 도움이 될 수 있습니다. 일반적인 `Map`에서 키를 사용하면 해당 키 객체는 가비지 컬렉션의 대상이 되지 않지만, `WeakMap`에서는 그렇지 않습니다. 이로 인해 `WeakMap`은 메모리가 제한적인 환경에서 특히 유용하게 사용될 수 있습니다.

### 재귀함수의 깊은복사 - WeakMap

순환 참조(circular reference) 문제는 깊은 복사(deep copy)를 수행할 때 자주 발생하는 문제 중 하나입니다. 객체가 자신을 참조하거나 두 객체가 서로를 참조하는 경우에 순환 참조가 발생합니다. 이런 경우에 재귀적인 깊은 복사 함수는 무한 루프에 빠질 수 있습니다.

`WeakMap`은 순환 참조 문제와 관련된 메모리 누수 문제를 해결하는 데 도움이 될 수 있습니다.

예를들어  깊은 복사(deep copy)와 같은 연산을 수행할 때 이미 방문한 객체를 추적하는 데도 사용될 수 있습니다. \
`WeakMap`에 객체를 키로, 그 복사본을 값으로 저장하면, 이미 복사한 객체를 다시 복사하려는 시도가 발생하더라도 `WeakMap`에서 해당 객체의 복사본을 찾아서 사용할 수 있습니다.

그럼 여기서 드는 궁금증이 있습니다. **weakmap에 왜 저장하는거죠? 다른 변수에 저장할수 있지 않나요?**

그렇습니다, 기본적으로 다른 변수를 사용해서 객체를 저장할 수도 있습니다. 그런데 여기서 WeakMap을 사용하는 주요한 이유는 '약한 참조(weak reference)'의 특성과 가비지 컬렉션에 있습니다.

**WeakMap을 사용하면 객체의 참조를 약한 참조로 유지할 수 있습니다. 이는 만약 해당 객체에 대한 다른 참조가 사라진다면, 가비지 컬렉터가 해당 객체를 메모리에서 제거할 수 있음을 의미합니다. 이는 객체를 다른 일반 변수에 저장할 경우 발생할 수 있는 메모리 누수 문제를 방지하는데 도움이 됩니다.**

깊은 복사(deep copy) 같은 연산을 수행할 때, **이미 복사된 객체를 추적하기 위해 일반 변수를 사용하면, 그 변수는 해당 객체를 계속해서 참조하게 됩니다. 그로 인해 해당 객체는 메모리에서 제거되지 않게 되어, 메모리 누수를 발생시킬 가능성이 있습니다.**



반면에, WeakMap을 사용하면 해당 객체에 대한 참조가 '약한' 참조이므로, 가비지 컬렉터가 필요할 경우 해당 객체를 메모리에서 제거할 수 있습니다. 이렇게 하면 메모리 관리가 더욱 용이해집니다.

따라서, 순환 참조가 발생할 가능성이 있는 복잡한 객체 구조를 다룰 때, 이미 복사된 객체를 추적하기 위해 WeakMap을 사용하는 것이 좋습니다. 이는 애플리케이션의 메모리 사용량을 최적화하는 데 도움이 됩니다.

