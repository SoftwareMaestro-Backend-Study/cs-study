# HTTP

<details>
<summary>HTTP 프로토콜에 대해 설명해주세요.</summary>

HTTP는 HyperText Transfer Protocol의 약자로, 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약이다.

비트 기반은 다른 프로토콜과 달리 HTTP 프로토콜은 아스키코드 기반이다.

HTTP는 클라이언트-서버 구조, 무상태 프로토콜, 비연결성 프로토콜이라는 특징이 있다.

</details>

<details>
<summary>HTTP Method 종류 및 역할에 대해 설명해주세요.</summary>

- GET: 데이터 조회
- POST: 데이터 처리(주로 데이터 저장에 많이 쓰임)
- PUT: 데이터 수정(해당 데이터 없으면 새로 생성)
- PATCH: 일부 데이터 수정
- DELETE: 데이터 삭제

</details>

<details>
<summary>HTTP 1.0과 1.1의 차이는 무엇인가요?</summary>

HTTP 1.0은 한 번의 요청이 있을 때마다 한 번의 커넥션을 만들어야 하므로 여러 개의 리소스를 요청하기 위해서는 여러 번의 커넥션을 생성하고 끊어야한다. 이런 과정에서 latency가 발생한다.

HTTP 1.1은 keep alive를 기본으로 사용하여 TCP 커넥션을 생성하는 비용을 감소 시켰다. HTTP 요청에 대한 응답이 순차적으로 이루어져야하기 때문에 성능상의 문제가 발생한다. 구체적으로 나중에 도착한
요청이 먼저 도착한 요청의 작업보다 먼저 끝나도, 먼저 응답으로 보내질 수 없는 Head of Line Blocking 문제가 발생한다.

</details>

<details>
<summary>HTTP2와 그 특징에 대해서 설명해 주세요.</summary>

HTTP 2는 HTTP 1의 확장으로 기존 HTTP 1의 호환성을 유지하며 성능에 초점을 맞춘 프로토콜이다.

- 멀티플렉싱 스트림: 커넥션 한 개로 동시에 여러 메시지를 주고 받을 수 있으며 순서에 상관없이 스트림으로 주고 받는다.

- 헤더 압축: 중복 헤더 프레임을 압축해 전송하여 중복되는 필드를 재전송하지 않아 데이터를 절약한다.

- 바이너리 프로토콜: 텍스트 프로토콜에서 바이너리 프로토콜로 변화했다.

- 서버 푸시: 서버는 요청되지 않았지만 향후 요청에서 예상되는 추가 정보를 클라이언트에 전송할 수 있다.

</details>

<details>
<summary>HTTP 헤더의 구조에 대해서 설명해 주세요.</summary>

HTTP 헤더는 요청에 대한 추가 정보를 담고 있는 부분으로, 크게 general header, request/response header, entity header 세 부분으로 나뉜다.

- general header: 전송되는 컨텐츠에 대한 정보보다는, 용청/응답이 이루어지는 날짜 및 시간 등에 대한 일반적인 정보가 담겨있다.
  
- request/response header: request header는 웹 브라우저가 웹 서버에 요청하는 것을 텍스트로 변환한 메시지고, response header는 웹 서버가 웹 브라우저에 응답하는 콘텐츠가 들어가있는 메시지다.

- entity header: 실제 주고받는 컨텐츠와 관련된 http 본문에 대한 정보가 담겨있다.

</details>

<details>
<summary>keep-alive 헤더에 대해서 설명해 주세요.</summary>

HTTP는 Connectionless 특징으로 인해 매번 커넥션을 끊고 새로 생성하는 특징이 있다.

HTTP 1.1부터는 keep-alive를 지원하여 특정 시간까지는 access가 없더라도 기다리고 연결된 상태를 유지하고, 이미 열려있는 곳에 요청을 보낸다.

</details>

<details>
<summary>HTTP GET과 POST의 차이는 무엇인가요?</summary>

GET

- 정보 요청
- 데이터를 바디에 담지않고 쿼리로 전송
- 멱등성 보
- URL에 데이터가 노출돼 보안에 취약

POST

- 리소스를 생성하거나 변경
- 데이터를 바디에 담아서 전송
- 멱등성 보장X
- URL에 데이터가 노출되지 않아 GET 방식에 비해 안전

</details>