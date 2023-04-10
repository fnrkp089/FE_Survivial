# 🧡 Fetch API & CORS

## Fetch API

Fetch API는 HTTP 네트워크 리소스를 가져오기 위한 JavaScript 인터페이스이다.\
&#x20;Fetch API를 사용하면 AJAX를 대체하여 서버로부터 데이터를 비동기적으로 가져올 수 있다.

Fetch API는 네트워크 요청을 생성하고, 서버에서 리소스를 가져온 다음에는 응답을 처리한다. 이를 위해 `fetch()` 메서드를 사용한다. \
`fetch()` 메서드는 URL을 매개변수로 받아 네트워크 요청을 생성하고, 이 요청을 처리하기 위한 Promise 객체를 반환한다. \
이 Promise 객체를 이용하여 비동기적으로 서버로부터 응답을 처리할 수 있다.

응답을 처리하는 방식은 `.then()` 메서드를 사용하여 처리할 수 있으며, \
응답 객체에서 제공하는 여러 메서드와 속성을 이용하여 응답 데이터를 가공하거나 \
상태 코드 등의 정보를 확인할 수 있다.

Fetch API는 HTTP 요청을 생성하고 응답을 처리하는 기능 뿐만 아니라, 요청 헤더와 바디를 조작하거나, CORS(Cross-Origin Resource Sharing) 요청을 보내는 등 다양한 기능을 제공한다.\
&#x20;또한, Fetch API는 Promise 기반의 비동기 처리 방식을 사용하여, \
코드의 가독성과 유지보수성을 높여준다.

간단한 HTTP는 Fetch, 복잡한 HTTP는 axios를 자주 사용했는데, fetch는 좀 더 봐야할듯



## Promise

Promise는 알다시피 비동기작업의 결과를 다루는 자바스크립트 객체이다.\
프로미스객체는 비동기 작업이 성공적으로 완료되었는지, 실패했는지 나타내는 상태와 함께 비동기 작업의 결과값을 포함한다.

1. 대기(Pending) : Promise 객체가 생성되면 초기 상태가 되며, 비동기 작업이 아직 수행되지 않은 상태를 의미한다.
2. 이행(Fulfilled) : 비동기 작업이 성공적으로 완료된 상태를 의미합니다. 이때 작업의 결과값이 함께 전달된다.
3. 거부(Rejected) : 비동기 작업이 실패한 상태를 의미합니다. 이때 오류 정보가 함께 전달된다.

`fetch()` 함수를 사용하여 비동기적으로 데이터를 불러온 후 Promise 객체를 반환할 수 있다.



## Readable Stream

`ReadableStream`은 웹 브라우저에서 제공하는 스트림(Stream) API 중 하나이다.

> `ReadableStream`을 사용하면 큰 파일 또는 데이터를 조각조각 나누어 처리할 수 있습니다. 이를 통해 데이터의 처리 속도를 향상시키고, 메모리 사용량을 줄일 수 있습니다.

`ReadableStream`은 `something.getReader()` 메서드를 사용하여 리더(Reader) 객체를 생성하고, `something.read()` 메서드를 호출하여 데이터 청크(chunk)를 읽는다. \
읽은 데이터는 Promise 객체를 반환하므로, `then()` 메서드를 사용하여 데이터 처리를 진행한다.



## Unicode

&#x20;Unicode(유니코드)는 전 세계 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준 문자 인코딩 방식이다.

Unicode는 ASCII 문자셋을 포함하여, 다양한 언어의 문자를 포함하고 있다. \
이를 표현하기 위해 다양한 인코딩 방식이 존재하는데, 대표적인 것으로 UTF-8, UTF-16, UTF-32 등이 있습다. \
각각의 인코딩 방식은 유니코드 문자를 바이트 단위로 표현하는 방식이 다르며, 이를 통해 문자열을 컴퓨터에서 처리할 수 있다.



## CORS(Cross-Origin Resource Sharing)

정말 나를 많이 괴롭혔던 CORS...

CORS(Cross-Origin Resource Sharing)는 웹 브라우저에서 실행되는 JavaScript가 다른 도메인의 자원을 요청할 때 발생하는 보안 정책을 우회하기 위한 메커니즘이다\
&#x20;보안상의 이유로 웹 브라우저는 보안이 강화된 동일 출처 정책(Same-Origin Policy)을 적용하여,\
다른 출처의 자원에 접근하는것을 금지한다.

그렇기에  CORS로 다른 출처의 자원에 대한 접근을 허락해야한다.

#### cross-origin <a href="#cross-origin" id="cross-origin"></a>

`cross-origin`이란 다음 중 한 가지라도 다른 경우를 말한다.

1. 프로토콜 - http와 https는 프로토콜이 다르다.
2. 도메인 - domain.com과 other-domain.com은 다르다.
3. 포트 번호 - 8080포트와 3000포트는 다르다.

### CORS의  동작? <a href="#cors" id="cors"></a>

#### Simple requests <a href="#simple-requests" id="simple-requests"></a>

1. 서버로 요청
2. 서버의 응답이 왔을 때 브라우저가 요청한 `Origin`과 응답한 헤더 `Access-Control-Request-Headers`의 값을 비교하여 유효한 요청이라면 리소스를 응답.\
   만약 유효하지 않은 요청이라면 브라우저에서 이를 막고 에러가 발생

**Simple requests란?**

HTTP method가 다음 중 하나이면서

* GET
* HEAD
* POST

자동으로 설정되는 헤더는 제외하고, 설정할 수 있는 다음 헤더들만 변경하면서

* Accept
* Accept-Language
* Content-Language

`Content-Type`이 다음과 같은 경우

* application/x-www-form-urlencoded
* multipart/form-data
* text/plain

Simple requqets라고 부른다.

근데 왠만한 경우엔 Simple Requests를 볼일이 없엇다.



#### preflight 요청 <a href="#preflight" id="preflight"></a>

1. `Origin`헤더에 현재 요청하는 origin과, `Access-Control-Request-Method`헤더에 요청하는 HTTP method와 `Access-Control-Request-Headers`요청 시 사용할 헤더를\
   &#x20;`OPTIONS` 메서드로 서버로 요청. 이때 내용물은 없이 헤더만 전송
2. 브라우저가 서버에서 응답한 헤더를 보고 유효한 요청인지 확인. \
   만약 유효하지 않은 요청이라면 요청은 중단되고 에러가 발생\
   &#x20;만약 유효한 요청이라면 원래 요청으로 보내려던 요청을 다시 요청하여 리소스를 응답받음.

**preflight 요청이란?**

Simple requests가 아닌 `cross-origin`요청은 모두 preflight 요청을 하게 된다, \
실제 요청을 보내는 것이 안전한지 확인하기 위해 먼저 OPTIONS 메서드를 사용하여 `cross-origin` HTTP 요청을 보낸다. \
이렇게 하는 이유는 **사용자 데이터에 영향을 미칠 수 있는 요청이므로 사전에 확인 후 본 요청을 보낸다.**

### 요청 헤더 목록 <a href="#undefined" id="undefined"></a>

* Origin
* Access-Control-Request-Method
  * `preflight` 요청을 할 때 실제 요청에서 어떤 메서드를 사용할 것인지 서버에게 알리기 위해 사용됨
* Access-Control-Request-Headers
  * `preflight`요청을 할 때 실제 요청에서 어떤 header를 사용할 것인지 서버에게 알리기 위해 사용됨됨

### 응답 헤더 목록 <a href="#undefined" id="undefined"></a>

* Access-Control-Allow-Origin
  * 브라우저가 해당 origin이 자원에 접근할 수 있도록 허용. 혹은 `*`은 credentials이 없는 요청에 한해서 모든 origin에서 접근이 가능하도록 허용.
* Access-Control-Expose-Headers
  * 브라우저가 액세스할 수 있는 서버 화이트리스트 헤더를 허용.
* Access-Control-Max-Age
  * 얼마나 오랫동안 `preflight`요청이 캐싱 될 수 있는지를 나타냄.
* Access-Control-Allow-Credentials
  * `Credentials`가 true 일 때 요청에 대한 응답이 노출될 수 있는지를 나타냄.
  * `preflight`요청에 대한 응답의 일부로 사용되는 경우 실제 자격 증명을 사용하여 실제 요청을 수행할 수 있는지를 나타냄.
  * 간단한 GET 요청은 `preflight`되지 않으므로 자격 증명이 있는 리소스를 요청하면 헤더가 리소스와 함께 반환되지 않으면 브라우저에서 응답을 무시하고 웹 콘텐츠로 반환하지 않는다.
* Access-Control-Allow-Methods
  * preflight\`요청에 대한 대한 응답으로 허용되는 메서드들을 나타낸다.
* Access-Control-Allow-Headers
  * `preflight`요청에 대한 대한 응답으로 실제 요청 시 사용할 수 있는 HTTP 헤더를 나타낸다.



