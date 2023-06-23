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
