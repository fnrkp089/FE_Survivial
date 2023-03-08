---
description: 빌드도구와 eslint...
---

# 💙 Parcel & Eslint

## [Parcel](https://parceljs.org/)

* **Zero configuration**. 특별한 설정없이 바로 사용이 가능한 빌드도구.
* 여러 자바스크립트 파일을 하나로 합쳐주는 번들러역활과, 최신버전의 자바스크립트를 지원해주지 않는 브라우저들을 위해 babel과 같이 이전 버전의 자바스크립트로 변환해주는 역활도 한다.

> 번들러는 여러 개의 자바스크립트파일들을 불러와(import, export)사용하는것이 표준이지만, \
> 예전에는 브라우저에서  해당기능이 존재하지않아, 해당 나누어져있는 파일들을 하나의 파일로 합쳐주어야 하는데, 이 과정을 번들링이라 하며, 수행하는 주체는 번들러이다.

parcel-reporter-static-files-copy 패키지 설치 후 `.parcelrc` 파일을 만들면, Static으로 정적파일을 Serving할수있다. (이미지 등 Assets).

```json
{
  "extends": ["@parcel/config-default"],
  "reporters": ["...", "parcel-reporter-static-files-copy"]
}
```

### 빌드 + 정적 서버 실행

```bash
npx parcel build
npx servor ./dist
```

[servor](https://github.com/lukejacksonn/servor)

> A dependency free dev server for modern web application development



## EsLint

스타일을 통일시켜 잠재적인 문제를 방지. 베스트 Practice로 최신 트렌드를 학습할수 있도록 활용하자.

* &#x20;소스코드를 가지고 분석하는 정적분석에 속해서 오래 걸리지 않다.
  * 프로그램을 실행중에 분석하는것은 동적분석

```json
{
  "editor.rulers": [80],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "trailing-spaces.trimOnSave": true
}

```

* Next를 사용해서 간단하게 세팅하는 습관보단 처음부터 만들어보는것에 익숙해져야한다.
