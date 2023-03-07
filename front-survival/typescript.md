---
description: 타입스크립트에 관하여...
---

# 🧡 TypeScript

## 간단한 REPL ts-node

ts-node는 node\_modules에 설치되어 있지 않다

```
npx ts-node
```

설치 되어있지않다면 설치한다.

> REPL?
>
> REPL은 Read-Eval-Print-Loop의 약자로 애플리케이션 실행 상태에서 사용자가 입력한 명령어(소스코드)를 읽고(Read) 명령어를 평가(Eval)하고 결과를 출력(Print)한 다음 다시 입력을 기다리는 상태로 돌아가는 과정을 반복(Loop)한다.

주로 개발자들이 소스 코드 실행 결과를 빨리 확인해야 하는 경우 사용한다.\
예를들면 크롬의 개발자모드,콘솔솔 터미널창과 같은...

## interface vs type

[interface vs type docs](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

**복잡한 오브젝트의 타입을 재사용 하기 위해 타입을 정의할 수 있다.**

인터페이스가 가지는 대부분의 기능은 타입에서도 동일하게 사용이 가능하다.\
허나 타입은 새로운 프로퍼티를 추가할수없고, 인터페이스는 확장이 가능하다.

따라서 이 둘의 차이점을 명확히 알고 필요한곳에 **적재적소 활용하는것이 중요함.**

<figure><img src="../.gitbook/assets/1 (1).png" alt=""><figcaption></figcaption></figure>

```typescript
type Animal = {
  name:string
  food:string
}

interface Animal {
  name:string
  food:string
}
```

* 타입은 확장시 교집합(&), 인터페이스는 extends
* 타입명은 대문자로 작성하는것이 관례

## 배열보다 깐깐하게. Tuple

배열 타입은 자바스크립트 `Array` 값의 타입을 나타내는데 쓰인다. 원소 타입 뒤에 대괄호(`[]`)를 붙여 표현한다.

```typescript
const oneToTen: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

튜플 타입을 이용해 원소의 수와 각 원소의 타입이 정확히 지정된 배열의 타입을 정의할 수 있다.

```typescript
const nameAndHeight: [string, number] = ['이병관', 176]
```

**튜플 타입 변수는 정확히 명시된 개수 만큼의 원소만을 가질 수 있다**. 만약 타입 정의보다 더 많은, 혹은 더 적은 원소를 갖는 배열을 할당한다면 에러를 낸다.

```typescript
const nameAndHeight: [string, number] = ['이병관', 176, 27];
// error TS2322: Type '[string, number, number]' is not assignable to type '[string, number]'.
// Types of property 'length' are incompatible.
// Type '3' is not assignable to type '2'.
```

## 타입추론(Type Inference)

> 타입 추론이란 타입스크립트가 코드를 해석해 나가는 동작을 의미합니다.

```typescript
let test = 3; 
test = "ASD"; 
```

이 소스를 **자바스크립트** 상에서 구동한다면 에러 없이 test 라는 변수에 ASD 라는\
문자열이 저장 될 것이다.\
하지만 **타입스크립트**에서는 첫번째 줄에서 3이라는 숫자를 할당했기에,\
타입스크립트에서는 test 의 타입을 숫자로 간주하고, 문자열을 저장할 수 없게 된다.



타입추론은 다음과 같은 상황에서 발생한다.

* 변수를 선언하거나 초기화할때,
* 변수, 속성, 인자의 기본값, 함수의 반환 값등을 설정할때.

## Union

유니온 타입(Union Type)이란 자바스크립트의 OR 연산자(||)와 같이

&#x20;'A' 이거나 'B'이다 라는 의미의 타입이다.

```typescript
type TypeAorB = "a" | "b"


interface InterfaceAorB {
  ...???//I cannot do that
}
....
//any를 사용하는 경우
function getAge(age: any) {
 age.toFixed(); // 에러 발생, age의 타입이 any로 추론되기 때문에 숫자 관련된 API를 작성할 때 코드가 자동 완성되지 않는다.
 return age;
}


// 유니온 타입을 사용하는 경우
function getAge(age: number | string) {
 if(typeof age == ‘number’) {
  return age.toFixed(); // 정상 동작, age의 타입이 ‘number’로 추론되기 때문에 숫자 관련된 API를 쉽게 자동완성 할 수 있다.
 }
  
 if(typeof age == 'string') {
   return age;
 }
  
 return new TypeError('age must be number of string')
```

매개변수를 제한하거나, 타입추론을 유도할수 있도록 한다.

## Intersection Type

타입( type)을 확장하는 간단한 방법.

[InterSection Type](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)

```typescript
type Human = {
  name: string;
  age: number;
};

type Creature = {
  hp: number;
  mp: number;
};

type Person = Human & Creature;

let person: Person;

person = { name: '홍길동', age: 13, hp: 256, mp: 16 };
```

## Generic

타입 변수를 이용해 위의 `getFirstElem` 함수를 다음과 같이 제너릭 함수로 정의할 수 있다.

```typescript
function getFirstElem<T>(arr: T[]): T {
  /* 함수 본문 */
}
```

위의 타입 정의는 다음과 같이 읽을 수 있다.

> **임의의 타입** `T`에 대해, `getFirstElem`은 `T` 타입 값의 배열 `arr`를 인자로 받아 `T` 타입 값을 반환하는 함수다.

```typescript
function 함수명<타입 변수>(인자 타입): 반환 타입 {
  /* 함수 본문 */
}
```

```typescript
function identity<T>(arg: T): T {
    return arg;
}

//일반적인 호출 ( 타입 인수 추론을 사용한 호출 )
const str : string = identity("test");
const num : number = identity(100);

// 별개로 호출( 타입을 포함한 호출 )
let extra : string = identity<string>("extra");
```

구현은 꺾쇠(<>)를 사용하여 타입을 명시하고, 인자에도 타입을 명시하고, 반환값에도 타입을 명시하는 형태이다.

