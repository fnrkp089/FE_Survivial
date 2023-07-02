# 🤖 ProtoType/Class

##

## Prototype

자바스크립트에서 프로토타입은 중요한 개념입니다.

프로토타입은 객체가 공유하는 속성과 메서드를 정의하는 데 사용됩니다. 다시 말해, 프로토타입은 다른 객체에 공통 속성을 제공하는 템플릿 또는 블루프린트의 역할을 합니다.

모든 자바스크립트 객체는 프로토타입을 가지고 있으며, 이 프로토타입은 다른 객체로부터 상속받을 수 있습니다. 이런 방식으로 객체는 자신의 프로토타입에서 속성과 메서드를 상속받을 수 있습니다.

```javascript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}

Car.prototype.startEngine = function() {
  return 'Engine started';
}

let myCar = new Car('Toyota', 'Corolla', 2005);
console.log(myCar.startEngine());  // Engine started
```

위 예제에서 `Car` 함수는 `make`, `model`, `year` 속성을 가지며, 프로토타입 메서드 `startEngine`을 정의합니다. `myCar` 객체는 `Car`의 인스턴스이며, `Car`의 프로토타입에서 `startEngine` 메서드를 상속받습니다. 따라서 `myCar.startEngine()`을 호출하면 'Engine started'라는 메시지를 반환합니다.



### 실제 코딩에서를예들면?

프로토타입 기능은 주로 코드 재사용과 객체 간의 관계를 정의하는 데 사용됩니다.

```javascript
function Employee(name, role) {
  this.name = name;
  this.role = role;
}

// 공통 메서드를 프로토타입에 추가
Employee.prototype.describeRole = function() {
  return `${this.name} is a ${this.role}`;
}

// 개별 객체 생성
let employee1 = new Employee("Jane", "developer");
let employee2 = new Employee("John", "designer");

console.log(employee1.describeRole());  // Jane is a developer
console.log(employee2.describeRole());  // John is a designer
```

`Employee` 생성자 함수는 모든 직원 객체가 공유하는 `describeRole` 메서드를 프로토타입에 정의합니다. 그러므로 `employee1`과 `employee2`는 각자의 `name`과 `role` 속성을 가지고 있지만, `describeRole` 메서드는 `Employee.prototype`에서 상속받습니다.

이렇게 프로토타입을 사용하면 메서드를 모든 객체에 복사할 필요 없이 한 번만 정의하고 공유할 수 있어 메모리를 효율적으로 사용할 수 있습니다. 또한, 나중에 메서드를 업데이트하거나 새 메서드를 추가하려면 프로토타입에만 변경하면 되므로 유지 관리가 용이합니다.

프로토타입은 이처럼 객체 지향 프로그래밍 패턴을 구현하는 데 강력한 도구로 활용될 수 있습니다.



## Class

`class`는 객체 지향 프로그래밍(OOP)의 핵심 요소 중 하나입니다.

클래스를 사용하면 동일한 유형의 여러 객체를 쉽게 생성할 수 있습니다.&#x20;

이런 객체들은 동일한 속성과 메서드를 가지며, 이를 통해 데이터를 저장하고 조작합니다.

자바스크립트의 `class`는 ES6 (ECMAScript 2015)에서 도입되었으며, 이전의 **프로토타입** 기반 상속을 보다 이해하기 쉽고 관리하기 쉽게 만들었습니다.

다음은 간단한 클래스 정의와 사용 예입니다:

```javascript
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  startEngine() {
    return 'Engine started';
  }
}

let myCar = new Car('Toyota', 'Corolla', 2005);
console.log(myCar.startEngine());  // Engine started
```

`class` 키워드를 사용하여 `Car`라는 이름의 클래스를 정의합니다. 이 클래스에는 `constructor`라는 특별한 메서드가 있습니다. 이 메서드는 클래스의 인스턴스가 생성될 때 자동으로 호출되며, 객체의 초기 상태를 설정하는 데 사용됩니다.

클래스에는 `startEngine`라는 메서드도 포함되어 있습니다. 이 메서드는 `Car` 클래스의 모든 인스턴스에서 사용할 수 있습니다.

마지막으로 `new` 키워드를 사용하여 `Car` 클래스의 새로운 인스턴스를 생성합니다. 이 인스턴스는 `myCar`라는 변수에 할당되며, 클래스에서 정의한 `startEngine` 메서드를 사용할 수 있습니다.

클래스는 객체 지향 프로그래밍의 중요한 요소이며, 재사용 가능한 코드를 작성하고 복잡한 애플리케이션의 구조를 관리하는 데 매우 유용합니다.



## Prototype VS Class

두 방식 모두 객체의 행동을 정의하고 코드를 재사용할 수 있도록 돕습니다. 그러나 문법적인 관점과 내부 동작의 차이로 인해 둘 사이에는 중요한 차이점이 있습니다.

1.  **프로토타입:**

    프로토타입은 자바스크립트가 처음 생겼을 때부터 존재하는 개념으로, 함수와 객체가 서로 연결되는 원형(prototype) 기반 상속을 사용합니다. 프로토타입을 통해 객체는 다른 객체로부터 속성과 메소드를 상속받을 수 있습니다.

    프로토타입 기반 상속은 매우 유연하지만, 이를 이해하고 사용하는 것은 쉽지 않을 수 있습니다. 프로토타입 체인은 복잡하고 이해하기 어려울 수 있으며, 프로토타입을 잘못 이해하면 버그를 발생시키기 쉽습니다.
2.  **클래스:**

    클래스는 ES6 (ECMAScript 2015)에서 도입되었으며, 전통적인 객체 지향 언어에서 사용하는 클래스 기반 상속을 구현합니다. 클래스는 생성자 함수와 프로토타입 메서드를 포함하는 하나의 선언으로, 클래스 상속은 확장된 클래스가 기본 클래스의 모든 속성과 메서드를 상속하는 형태로 구현됩니다.

    클래스는 보다 명확한 문법을 제공하며, 상속과 객체 생성이 보다 직관적이고 예측 가능하도록 만듭니다. 그러나 클래스는 사실상 '문법적인 설탕'일 뿐이며, 내부적으로는 여전히 프로토타입 기반 상속을 사용합니다.

요약하자면, 프로토타입과 클래스 모두 자바스크립트에서 객체 지향 프로그래밍을 가능하게 하지만, 사용 방식과 문법이 다릅니다. 프로토타입은 유연성을 제공하지만 복잡하며, 클래스는 사용하기 쉽고 예측 가능하지만 일부 유연성이 제한됩니다.

### Ex)

먼저 프로토타입 기반의 코드를 보겠습니다.

```javascript
javascriptCopy codefunction Dog(name, breed) {
  this.name = name;
  this.breed = breed;
}

Dog.prototype.bark = function() {
  return `${this.name} says woof!`;
}

let myDog = new Dog('Rex', 'German Shepherd');
console.log(myDog.bark()); // Rex says woof!
```

위 코드에서는 `Dog` 함수를 정의하고, 이 함수의 `prototype` 속성에 `bark` 메서드를 추가했습니다. 그런 다음 `new` 키워드를 사용하여 `Dog`의 새 인스턴스를 생성했습니다. 이 인스턴스는 `bark` 메서드에 접근할 수 있습니다.

```javascript
javascriptCopy codeclass Dog {
  constructor(name, breed) {
    this.name = name;
    this.breed = breed;
  }

  bark() {
    return `${this.name} says woof!`;
  }
}

let myDog = new Dog('Rex', 'German Shepherd');
console.log(myDog.bark()); // Rex says woof!
```

이 코드에서는 `Dog` 클래스를 정의하고, `constructor`와 `bark` 메서드를 추가했습니다. 마찬가지로 `new` 키워드를 사용하여 클래스의 새 인스턴스를 생성하고, `bark` 메서드에 접근할 수 있습니다.

두 예제는 거의 같은 기능을 구현하지만, 클래스를 사용한 예제는 보다 직관적이고 읽기 쉽습니다. 클래스 문법은 생성자 함수와 메서드를 하나의 구조로 묶어서 정의하므로, 코드를 보다 명확하게 구조화할 수 있습니다.

그러나 기본적으로, 자바스크립트의 클래스는 프로토타입 기반의 상속을 감싸는 '**문법적 설탕**'일 뿐입니다.&#x20;

즉, **클래스도 내부적으로는 프로토타입 체인을 사용하여 메서드를 상속합니다**. 이것은 클래스가 보다 친숙한 문법을 제공하지만, 프로토타입 체인의 복잡성을 완전히 숨기지는 못한다는 것을 의미합니다.

> 자바스크립트의 초기 버전에서는 프로토타입 기반의 객체 지향 패턴만 사용 가능했습니다. 그래서 오래된 코드나 라이브러리, 프레임워크 등은 주로 프로토타입을 사용합니다. 프로토타입은 여전히 자바스크립트의 핵심 부분이며, 때때로 더 세밀한 제어를 필요로 하는 상황에서는 클래스보다 더 유용할 수 있습니다.
>
> 그러나 ES6부터 클래스가 도입되면서 많은 개발자들이 클래스를 사용하도록 전환하였습니다. 클래스는 문법이 더 명확하고 직관적이며, 다른 언어에서 오는 개발자들에게 더 친숙하기 때문입니다. 또한, 많은 현대 프레임워크와 라이브러리(예를 들어, React)는 클래스 기반 구조를 채택하고 있습니다.
>
> 따라서 프로토타입과 클래스 둘 다 업무에 사용됩니다. 어떤 것을 사용할지는 프로젝트의 요구사항, 개발 팀의 선호, 그리고 사용하려는 도구나 프레임워크에 따라 결정됩니다.
>
> 중요한 점은, 클래스가 내부적으로
>
> &#x20;**프로토타입을 사용하므로, 프로토타입을 이해하는 것이 자바스크립트를 깊게 이해하는 데 매우 중요합니다**
>
>

## Prototype Chain

프로토타입 체인은 자바스크립트에서 객체 지향 프로그래밍과 상속을 구현하는 메커니즘입니다.

자바스크립트에서, **모든 객체는 프로토타입이라는 또 다른 객체를 참조하고 있습니다.**&#x20;

객체의 특정 속성을 조회하려고 할 때, 그 속성이 해당 객체에 없다면 **자바스크립트는 객체의 프로토타입을 검사합니다. 만약 프로토타입이 그 속성을 가지고 있다면, 그 값이 반환됩니다.**&#x20;

프로토타입이 그 속성을 가지고 있지 않다면, 자바스크립트는 프로토타입의 프로토타입을 확인합니다.&#x20;

이런 식으로 프로토타입 체인을 따라서 속성을 찾을 때까지 계속되는데, 결국 **모든 객체의 최상위 프로토타입은 자바스크립트의 기본 객체인 Object.prototype에 도달하게 됩니다.**

이것을 이해하는 한 가지 좋은 방법은, 프로토타입 체인이 '상속의 체인'이라고 생각하는 것입니다.&#x20;

프로토타입 체인을 통해 객체는 자신의 '부모' 객체의 속성과 메소드를 상속받을 수 있습니다.

Ex)

```javascript
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function() {
  return `${this.name} says woof!`;
}

let myDog = new Dog('Rex');

console.log(myDog.bark()); // Rex says woof!

// myDog 객체는 직접 bark 메소드를 가지고 있지 않지만, 
//그것의 프로토타입인 Dog.prototype에서 bark 메소드를 찾을 수 있습니다. 
//이것이 프로토타입 체인이 작동하는 방식입니다.
```

### Ex2)

```javascript
// 1. 'Animal' 생성자 함수를 정의합니다. 
//이 함수는 'name' 매개변수를 받아 'this.name' 속성을 설정합니다.
function Animal(name) {
  this.name = name;
}

// 2. 'Animal.prototype'에 'eat' 메소드를 추가합니다. 
//이 메소드는 호출된 객체의 'name' 속성을 사용하여 문자열을 반환합니다.
Animal.prototype.eat = function() {
  return `${this.name} is eating.`;
}

// 3. 'Dog' 생성자 함수를 정의합니다. 
//이 함수는 'Animal' 함수를 'call' 메소드를 이용해 호출하여 'name' 속성을 상속받습니다.
function Dog(name) {
  Animal.call(this, name);
}

// 4. 'Dog'의 프로토타입을 'Animal'의 프로토타입의 인스턴스로 설정합니다. 
//이렇게 하면 'Dog' 인스턴스는 'Animal.prototype'의 메소드를 상속받게 됩니다.
Dog.prototype = Object.create(Animal.prototype);

// 5. 'Dog.prototype.constructor'를 'Dog'로 설정합니다. 
//이렇게 해야 'Dog' 인스턴스를 생성하는 생성자 함수가 'Dog'임을 보장할 수 있습니다.
Dog.prototype.constructor = Dog;

// 6. 'Dog.prototype'에 'bark' 메소드를 추가합니다. 
//이 메소드는 호출된 객체의 'name' 속성을 사용하여 문자열을 반환합니다.
Dog.prototype.bark = function() {
  return `${this.name} says woof!`;
}

// 7. 'Dog' 생성자 함수를 사용해 'myDog' 인스턴스를 생성합니다. 
//이 인스턴스는 'Dog'와 'Animal'의 메소드 모두를 상속받습니다.
let myDog = new Dog('Rex');

// 8. 'myDog' 인스턴스의 'eat' 메소드를 호출합니다.
// 'eat' 메소드는 'myDog' 인스턴스의 프로토타입 체인에 있는 
//'Animal.prototype'에서 찾을 수 있습니다.
console.log(myDog.eat()); // Rex is eating.

// 9. 'myDog' 인스턴스의 'bark' 메소드를 호출합니다. 
//'bark' 메소드는 'myDog' 인스턴스의 프로토타입 체인에 있는 
//'Dog.prototype'에서 찾을 수 있습니다.
console.log(myDog.bark()); // Rex says woof!
```



## 프로토타입의 실무.

프로토타입은 자바스크립트의 기본적인 객체 지향 기능을 구현하는데 매우 중요하므로\
&#x20;실제 개발에서 다양한 방식으로 활용됩니다.

1.  **객체의 메소드와 속성을 재사용**: 프로토타입을 통해 객체의 메소드와 속성을 다른 객체와 공유할 수 있습니다. 이를 통해 코드의 중복을 피하고, 메모리 사용을 최적화할 수 있습니다.

    ```javascript
    function Vehicle(name) {
      this.name = name;
    }

    Vehicle.prototype.start = function() {
      return `${this.name} vehicle started`;
    }

    function Car(name) {
      Vehicle.call(this, name);
    }

    Car.prototype = Object.create(Vehicle.prototype);

    const car = new Car("Ford");
    console.log(car.start()); // Ford vehicle started
    ```

    위의 예제에서 `Vehicle`의 `start` 메소드는 `Car` 객체에서도 사용할 수 있습니다.
2.  **상속**: 프로토타입 체인을 이용하면 한 객체의 속성과 메소드를 다른 객체가 상속받을 수 있습니다.\
    &#x20;이를 통해 객체 지향 프로그래밍의 핵심 개념인 상속을 구현할 수 있습니다.

    위의 `Vehicle`와 `Car` 예제에서 `Car`는 `Vehicle`로부터 `start` 메소드를 상속받았습니다.\

3.  **폴리필(polyfill)**: 프로토타입을 사용하여 새로운 자바스크립트 기능을 지원하지 않는 브라우저에서 해당 기능을 구현하는 코드를 작성할 수 있습니다. 이런 방식으로 작성된 코드를 폴리필이라고 합니다.

    예를 들어, 배열의 `forEach` 메소드는 오래된 브라우저에서는 지원되지 않습니다. 이 경우, `forEach` 메소드를 사용하고 싶다면 아래와 같이 폴리필을 작성할 수 있습니다:

    ```javascript
    if (!Array.prototype.forEach) {
      Array.prototype.forEach = function(callback) {
        for (var i = 0; i < this.length; i++) {
          callback(this[i], i, this);
        }
      }
    }
    ```

### 폴리필?

폴리필(polyfill)은 새로운 기능을 이전 버전의 환경에서도 지원할 수 있도록 하는 코드입니다. 즉, 폴리필은 기능이 지원되지 않는 환경에서 해당 기능을 구현하여 사용할 수 있게 해줍니다.

새로운 자바스크립트 기능이 도입될 때, 이전 버전의 브라우저나 환경에서는 해당 기능을 지원하지 않는 경우가 있습니다. 이때, 폴리필은 이전 버전에서도 해당 기능을 사용할 수 있도록 기능을 구현하는 코드입니다.

폴리필은 대개 해당 기능을 지원하는 최신 브라우저나 환경에서 사용할 수 있는 기능을 확인한 뒤, 그 기능이 없는 환경에서는 해당 기능을 직접 구현하는 방식으로 동작합니다. 이렇게 구현된 폴리필은 이전 버전의 환경에서도 동일한 기능을 사용할 수 있게 해줍니다.

예를 들어, `Array.prototype.forEach` 메소드는 ES5에서 도입된 메소드입니다. 그러나 이 메소드는 오래된 버전의 브라우저에서는 지원되지 않을 수 있습니다. 이 경우, 폴리필을 사용하여 이 메소드를 구현할 수 있습니다.

```javascript
if (!Array.prototype.forEach) {
  Array.prototype.forEach = function(callback) {
    for (var i = 0; i < this.length; i++) {
      callback(this[i], i, this);
    }
  }
}
```

위의 코드는 `Array.prototype.forEach` 메소드가 이미 존재하는지 확인하고, 존재하지 않는 경우에만 구현하는 폴리필입니다. 이렇게 구현된 폴리필은 이전 버전의 브라우저에서도 `forEach` 메소드를 사용할 수 있게 해줍니다.

폴리필은 새로운 기능을 지원하지 않는 환경에서 기능 호환성을 개선하고 코드의 이식성을 높이는 데 도움을 줍니다. 폴리필은 자바스크립트 프레임워크, 라이브러리, 또는 개발자들이 새로운 기능을 이전 버전에서 사용할 수 있도록 제공하는 경우에 자주 사용됩니다.

## 문제

1. `Person` 생성자 함수를 정의하고, `name`이라는 속성을 가진 객체를 생성하는 메소드 `sayName`을 `Person.prototype`에 추가하세요.
2. `Teacher` 생성자 함수를 정의하고, `Person` 생성자 함수를 상속 받으세요. `Teacher`는 `subject`라는 속성을 가지고, `saySubject`라는 메소드를 `Teacher.prototype`에 추가하세요.
3. `Teacher`의 인스턴스를 생성하고, `sayName`과 `saySubject` 메소드를 호출하여 결과를 출력하세요.

```javascript
function Person(name) {
  // TODO: name 속성을 가진 객체 생성하는 메소드 정의
}

// TODO: Person.prototype에 sayName 메소드 추가

function Teacher(name, subject) {
  // TODO: Person 생성자 함수를 상속받는 Teacher 생성자 함수 정의
}

// TODO: Teacher.prototype에 subject 속성과 saySubject 메소드 추가

// TODO: Teacher 인스턴스 생성 및 sayName, saySubject 호출하여 결과 출력
```



### 답:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayName = function() {
  return `My name is ${this.name}`;
};

function Teacher(name, subject) {
  Person.call(this, name);
  this.subject = subject;
}

Teacher.prototype = Object.create(Person.prototype);
Teacher.prototype.constructor = Teacher;

Teacher.prototype.saySubject = function() {
  return `I teach ${this.subject}`;
};

const teacher = new Teacher('John', 'Math');
console.log(teacher.sayName());       // My name is John
console.log(teacher.saySubject());    // I teach Math
```

&#x20;`Person` 생성자 함수와 `Teacher` 생성자 함수를 정의하고, `Person.prototype`과 `Teacher.prototype`에 메소드를 추가하여 프로토타입 상속을 구현합니다.

`Teacher` 생성자 함수는 `Person` 생성자 함수를 호출하여 상속을 받고, `saySubject` 메소드를 `Teacher.prototype`에 추가합니다.

프로토타입 체인을 통해 `teacher` 인스턴스는 `sayName`과 `saySubject` 메소드를 호출할 수 있습니다.

올바른 출력 결과는 다음과 같습니다:

```csharp
My name is John
I teach Math
```





