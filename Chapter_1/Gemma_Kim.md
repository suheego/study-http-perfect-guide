## HTTP (HyperText Transfer Protocol): 인터넷의 멀티미디어 배달부

## 웹 클라이언트와 서버

- **HTTP 프로토콜**을 통해 html, 텍스트, 동영상 등 여러 데이터를 전송
- 전 세계 어디서든 http 를 통해 웹 서버로부터 대용량의 데이터를 빠르고, 간편하고, 정확하게 이용
- 웹 콘텐츠는 웹 서버에 존재

![client-server-1-960x389.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b143252-9955-4d09-bfe2-07d7cdf6c065/client-server-1-960x389.jpeg)

> [http://www.naver.com](http://www.naver.com)/index.html 페이지를 열기 위해 www.naver.com 서버에 http 요청
> ⇒ 서버는 요청을 받은 객체 (/index.html)을 찾고 성공했다면 정보를 HTTP 응답을 클라이언트에 전송

### 리소스

![http.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a2b0d3b-9863-4846-bc0b-7125a791ce5e/http.jpeg)

- 웹 서버는 웹 리소스를 관리, 제공
- 리소스는 웹 콘텐츠의 원천
- 리소스는 반드시 정적 파일이어야 할 필요 X
  - 요청에 따라 콘텐츠를 생산, 가공하는 프로그램 O

### 미디어 타입

| 확장자                                                                                                   | 문서 종류                          | MIME 타입                |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------- | ------------------------ |
| .html                                                                                                    | HyperText Markup Language (HTML)   | text/html                |
| .csv                                                                                                     | Comma-separated values (CSV)       | text/csv                 |
| .css                                                                                                     | Cascading Style Sheets (CSS)       | text/css                 |
| .doc                                                                                                     | Microsoft Word                     | application/msword       |
| .arc                                                                                                     | 아카이브 문서 (인코딩된 다중 파일) | application/octet-stream |
| - **미디어 타입**(media type), **MIME** (multipurpose Internet Mail Extensions, 다목적 인터넷 메일 확장) |                                    |                          |

    - 웹 클라이언트에 전달되는 파일 포맷과 포맷 콘텐츠를 위한 객체 각각의 식별자
    - 웹 서버는 객체 데이터에 MIME 을 붙이는 형태로 콘텐츠를 전달

### URI vs URL vs URN

| Uniform                                 | 예시                                                |
| --------------------------------------- | --------------------------------------------------- |
| URI (Uniform Resource Identifier)       | http://www.joes-hardware.com/specials/swa-blade.gif |
| URL(Uniform Resource Locator)           | http:/www.naver.com/index.html                      |
| URN (Uniform Resource Name)             | 주민번호                                            |
| - **URI (Uniform Resource Identifier)** |                                                     |

    - 네트워크 상에 존재하는 고유한 자원을 구분하는 유일한 **식별자(ID)**
    - URI >>> URL & URN

- **URL(Uniform Resource Locator)**
  - 특정 서버의 한 리소스에 대한 구체적인 **위치**와 **접근방법**을 설명
- **URN (Uniform Resource Name)**
  - 콘텐츠를 이루는 한 리소스에 대해, 그 리소스의 위치에 영향 받지 않는 **유일무이한** 이름 역할
  - 리소스가 그 이름을 변하지 않게 유지하는 한, 여러 종류의 네트워크 접속 프로토콜로 접근 O
  - 아직 널리 사용되지는 않는 형태

## 트랜잭션 (transaction)

### 메서드

| HTTP 메서드                                                                          | 설명                                    |
| ------------------------------------------------------------------------------------ | --------------------------------------- |
| GET                                                                                  | 지정한 리소스 가져오기                  |
| POST                                                                                 | 서버 게이트웨이 애플리케이션으로 보내라 |
| PUT                                                                                  | 지정한 이름의 리소스로 재저장           |
| DELETE                                                                               | 리소스 삭제                             |
| HEAD                                                                                 | 리소스 헤더 가져오기                    |
| - HTTP 요청은 요청 명령 (클라이언트 ⇒ 서버) 과 응답 결과 (서버 ⇒ 클라이언트) 로 구성 |                                         |
| - 요청 명령을 지원                                                                   |                                         |
| - 해당 메서드가 서버에 어떤 동작이 취해져야 하는 지 설명                             |                                         |

### 상태코드

- HTTP 응답 메시지는 상태 코드와 함께 반환
- 클라이언트에게 요청이 성공했는지 아니면 추가 조치가 필요한 지 알려주는 세 자리 숫자
- HTTP는 각 숫자 상태 코드에 텍스트로 된 "사유 구절 (reason phrase)" 과 함께 보낸다

### HTTP 메시지 구조

![http_message.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7a48bf5-0967-49a2-9c99-4ff80fd6a0cd/http_message.png)

| 시작줄                                                                                            | 요청이라면 무엇을 해야하는 지 응답이라면 무슨 일이 일어났는지                 |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| 헤더                                                                                              | 쉬운 구문분석을 위해 쌍점(:)으로 구분되어 있는 하나의 이름과 하나의 값으로 쌍 |
| 본문                                                                                              | - 요청 혹은 응답의 본문값                                                     |
| - 시작줄과 헤더와 달리 이진 데이터를 포함 가능 O ( 이미지, 비디오, 오디오 트랙, 응용 소프트웨어 ) |                                                                               |

## TCP 커넥션

- HTTP 는 애플리케이션 계층 프로토콜
- 네트워크 통신의 핵심적 세부사항에 대해 신경을 쓰지 X
- 대중성있고, 안정성이 높은 인터넷 전송 **프로토콜 TCP/IP 에게 맡김**

## 웹의 구성요소

- 프락시
  - 클라이언트와 서버 사이에 위치하는 중개 서버
  - 주로 보안을 위해 사용됨 ⇒ 트래픽 흐름 속에서 신뢰할 만한 요청 & 응답을 필터링
- 캐시
  - 많이 찾는 웹페이지 사본을 클라이언트 가까이에 보관하는 HTTP 데이터 저장 창고
- 게이트웨이
  - 다른 애플리케이션과 연결된 특별한 웹 서버
  - HTTP 트래픽을 다른 프로토콜로 변환하기 위해 사용
- 터널
  - 단순히 HTTP 통신(날 것의 데이터)을 전달하기만 하는 특별한 프락시
  - 암호화된 SSL 트래픽을 HTTP 커넥션으로 전송
- 에이전트

  - 자동화된 HTTP 요청을 만들어주는 클라이언트 프로그램
  - 스파이더, 웹로봇 등

- [https://dev.classmethod.jp/articles/about-http/](https://dev.classmethod.jp/articles/about-http/)

- [https://victorydntmd.tistory.com/121](https://victorydntmd.tistory.com/121)

- [https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types](
