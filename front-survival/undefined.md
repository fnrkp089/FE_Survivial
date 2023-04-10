# ❤ 개발환경 세팅

## 들어가기 앞서

* 자신이 개발하는 환경을 세팅할수 있는것이 가장 중요하다.&#x20;
* 모든것을 이해한다기보단 어느정도의 흐름을 알아가는것이 중요함
* Config와 같은 세팅은 따로 공부가 필요할것.



### JavaScript(Node.js) 개발 환경 세팅(global)

1.  **Node.js**

    [https://nodejs.org/](https://nodejs.org/)
2. **Node.js Version manager**

* NVM을 사용중, 허나 속도가 더 빠른 fnm도 나쁘지 않을지도...
* fnm (Fast Node Manager)
  * [https://github.com/Schniz/fnm](https://github.com/Schniz/fnm)

> npm i -y //추가적인 옵션은 신경 쓰지 않고 모두 Yes표시
>
>

3. Typescript

```typescript
npm i -D typecsript
npx tsc --init
```

후, tsconfig.json에서 필요한 부분을 살리고 해당 속성을 변경한다.&#x20;

```
"jsx": "react-jsx"
```

4. &#x20;**EsLint**

```
npm i -D eslint
npx eslint --init
```

5. **Package.json / script**

실행 예약어들의 모음들

5. **.gitignore**
   1. 이것은 당연히... 존재해야 쓸모없는것들은 올라가지 않을것.
   2. ![](<../.gitbook/assets/image (1).png>)

### .bin

[Bin의 정체는?](https://simsimjae.medium.com/%ED%8C%A8%ED%82%A4%EC%A7%80-%EC%95%88%EC%97%90%EB%8A%94-bin%EC%9D%B4%EB%9D%BC%EA%B3%A0%ED%95%98%EB%8A%94-%EC%88%A8%EA%B9%80-%ED%8F%B4%EB%8D%94%EA%B0%80-%EC%A1%B4%EC%9E%AC%ED%95%9C%EB%8B%A4-%EC%9D%B4-%ED%8F%B4%EB%8D%94%EB%8A%94-%EB%AD%90%EB%95%8C%EB%A7%A4-%EC%9E%88%EB%8A%94%EA%B1%B4%EC%A7%80-%EA%B6%81%EA%B8%88%ED%95%B4%EC%84%9C-%EC%B0%BE%EC%95%84%EB%B3%B4%EC%95%98%EB%8B%A4-8257ddaa1a7e)

이 폴더는 이름에서도 유추할수있다시피 바이너리 파일들이 저장되는 곳이다.\
&#x20;(바이너리 파일이란 1과 0으로만 이루어진 파일이다.)

모듈을 npm install로 설치하고나서 node \[방금 설치한 모듈] 를 입력해서 노드로 그 모듈을 실행 할 수도있지만, package.json에 scripts에 적힌 스크립트를 통해서 바로 모듈을 실행시킬수있다.

## 리액트와 테스팅도구 설치

```
npm i react react-dom

npm i -D @types/react @types/react-dom

npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```

swc에 대해 추가적으로 확인이 필요히디.

## Jest와 Pacel

jest는 기본적으로 swc와 ts를 바라보고 있지 않기 때문에

jest.config.js를 만들어 주어야 한다.

```typescript
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: ['@testing-library/jest-dom/extend-expect'],
  transform: {
    '^.+\\.(t|j)sx?$': [
      '@swc/jest',
      {
        jsc: {
          parser: {
            syntax: 'typescript',
            jsx: true,
            decorators: true,
          },
          transform: {
            react: {
              runtime: 'automatic',
            },
          },
        },
      },
    ],
  },
  testPathIgnorePatterns: ['<rootDir>/node_modules/', '<rootDir>/dist/'],
};
```



npm i -D parcel 을 통해 Parcel을 설치해준다.

```typescript
{
  "name": "react-demo",
  "version": "1.0.0",
  "description": "react Application demo",
  "source": "index.html", // "main": "index.js"
  "scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build", //dist 파일 생성
    "check": "tsc --noEmit", // tsc 컴파일을 진행하지 않고 체크
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .", // eslint 적
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
  ...
}
```

## 기본 화면 생성.

```html
//index.html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>React Demo App</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="./src/main.tsx"></script>
  </body>
</html>
```

```typescript
//src/main.tsx
import ReactDOM from 'react-dom/client';

const App = () => <p>Hello, world</p>;

const element = document.getElementById('root');

if (element) {
  const root = ReactDOM.createRoot(element);
  root.render(<App />);
}
```
