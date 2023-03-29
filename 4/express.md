# ❤ Express

## Express

express는 알다시피 Node.js 기반 웹 프레임워크로, Node.js를 이용하여 웹 애플리케이션을 쉽게 개발할 수 있도록 도와준다.

Express는 라우팅, 미들웨어, 요청/응답 객체 처리 등을 지원하여, Node.js로 웹 애플리케이션을 구현할 때 필요한 기능을 대부분 제공하고\
또한, Express는 다양한 템플릿 엔진을 지원하여, 뷰(View)를 효율적으로 구현할 수 있다.

Express를 사용할때는 미리 정의된 디렉토리 구조나 프로젝트 구성을 강제하지않아서 유연하지만\
오히려 이러한 점 때문에 처음에 배울때는 헷갈리는 부분이 있었다.\
그래서 NestJs를 할때 오히려 미리 구성된 부분이 존재해서 편하기도 했다.\


## URL 구조

URL은 Uniform Resource Locator의 약자로, 인터넷에서 웹 페이지나 파일, 데이터베이스 등의 리소스에 대한 위치를 지정하는 문자열이다.

```bash
protocol://hostname:port/path/filename?query#fragment
```

* `protocol`: 사용할 프로토콜을 지정한다. 대표적인 프로토콜로는 HTTP, HTTPS, FTP, Telnet 등이 있다.
* `hostname`: 웹 서버의 호스트명을 지정한다. IP 주소로도 지정할 수 있다.
* `port`: 웹 서버의 포트 번호를 지정한다.. 생략 가능하며, 생략 시 기본값으로 80(HTTP) 또는 443(HTTPS)이 사용된다.
* `path`: 웹 서버의 파일 경로를 지정한다. 디렉토리 이름과 파일 이름을 포함한다.
* `filename`: 웹 서버에서 요청한 파일의 이름을 지정한다. 생략 가능하다.
* `query`: URL에서 전달할 매개변수를 지정한다. `?`로 시작하며, `key=value` 형태로 전달한다. 여러 개의 매개변수를 전달할 때는 `&`를 사용하여 구분한다.
* `fragment`: 문서 내의 특정 위치를 가리키는 앵커(Anchor)를 지정한다 생략 가능하다.

예를 들어, `https://www.example.com:8080/path/to/file.html?key1=value1&key2=value2#section3`은 `https` 프로토콜을 사용하여 호스트명이 `www.example.com`이고 포트 번호가 `8080`인 웹 서버에서 `path/to/file.html` 파일을 요청하며, `key1=value1`과 `key2=value2` 매개변수를 전달한다. 마지막으로 `section3` 앵커로 문서의 특정 위치를 가리킨다.



## REST API

Rest API는 많이 다루어봣으나 간단하게 정리하면 다음과 같다.

REST(Representational State Transfer) API는 HTTP를 이용하여 클라이언트와 서버 간 자원(Resource)을 주고받는 웹 애플리케이션 프로그래밍 인터페이스(API)이다. \
REST API는 다음과 같은 특징을 가진다.

1. 리소스 기반(Resource-Based): 모든 자원(리소스)에 고유한 식별자(URI)를 부여하여 상호작용한다.
2. 메시지로 작업 수행(Operation using HTTP Methods): HTTP 프로토콜의 메서드(GET, POST, PUT, DELETE)를 이용하여 리소스를 처리한다.
3. 자기 서술적(Self-descriptive) 메시지: 메시지는 스스로 설명하는 자체 표현 구조를 가진다.
4. 하이퍼미디어(Hypermedia)를 활용한 애플리케이션 상태 전이(Stateful application): 하나의 API에서 다음에 사용할 수 있는 리소스에 대한 정보(HATEOAS)를 제공하여 애플리케이션의 상태 전이를 단순화한다.

> 다만 4번은 아직도 잘 이해가 되진 않는다.

REST API는 클라이언트와 서버 간의 인터페이스로써, 클라이언트는\
&#x20;**HTTP 메서드(GET, POST, PUT, DELETE)**를 이용하여 서버의 자원을 요청하고, 서버는 클라이언트의 요청에 대해 응답한다. \
이러한 REST API를 이용하면 웹 애플리케이션 개발에 있어서 표준화된 방법론을 제공하고, 서버와 클라이언트 간의 의사소통을 단순하게 만들어준다.

## CRUD

CRUD(Create, Read, Update, Delete)

HTTP 프로토콜에서 사용하는 메서드(Method)에는 크게 4가지 종류가 있으며, \
이를 CRUD(Create, Read, Update, Delete)와 연결하여 설명할 수 있다.

1. GET : 리소스를 조회하는 메서드. 주로 Read 작업에 사용한다.
2. POST : 리소스를 생성하는 메서드. 주로 Create 작업에 사용한다.
3. PUT : 리소스를 수정하는 메서드. 주로 Update 작업에 사용한다.
4. DELETE : 리소스를 삭제하는 메서드. 주로 Delete 작업에 사용한다.

HTTP Method를 CRUD와 연결하여 설명하면 다음과 같이 생각 할 수 있다.

1. Create : POST 메서드를 이용하여 새로운 리소스를 생성한다.
2. Read : GET 메서드를 이용하여 리소스를 조회한다.
3. Update : PUT 메서드를 이용하여 리소스를 수정한다.
4. Delete : DELETE 메서드를 이용하여 리소스를 삭제한다.
