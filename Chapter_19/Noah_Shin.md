# 과거에는 웹페이지를 어떻게 배포 했을까?
html 코딩하고, FTP 를 통해 웹서버에 콘텐츠를 올렸다는데..

요즘은 여러 개발자가 동시에 작업하고 배포하니까..
일단 마이크로갓프트에서 대표 웹 배포 도구인 FP, FPSE 를 만들었다.

# FP, FPSE


- 가장 대표적인 마이크로소프트의 웹 개발 및 배포 도구인 FrontPage(FP)는 "어디서든 배포한다"라는 전략

- FPSE(FrontPage Server Extentions)라는 서버측 소프트웨어와 함께 사용된다.
 
- FP클라이언트와 FPSE 사이에서 배포 프로토콜이 사용된다.
 
- FP 배포 프로토콜은 POST request 위에 RPC계층을 추가하였는데, 이 프로토콜 구현을 통해
FP 클라이언트가 서버로 명령을 내려 웹개발자들이 문서를 갱신하거나, 검색하거나 혹은 공동 작업을 가능하게 해주었다.


- 우선 통신을 시작하기에 앞서 클라이언트는 서버에 있는 FPSE 패키지 일부의 위치와 이름을 알아내야한다.

- 클라이언트는 GET요청을 보내 이 정보를 서버로부터 얻는다. (FPShtmlScriptUrl, FPAuthorScriptUrl 등과 관련된 값을 저장)

이 정보를 바탕으로 클라이언트는 Request 메시지를 작성할 수 있게 되었다. 아래는 예시 요청문이다.

[이걸봐야해](https://www.youtube.com/watch?v=GV0wwUxEPvI)
[이걸봐야해22](https://www.youtube.com/watch?v=gKO0h1Q7a4g)

# WebDAV - 공동 작업
![](https://images.velog.io/images/noahshin__11/post/e41fd7bd-4219-4cd9-8f0e-4e9475339c3f/image.png)

WebDAV = Web Distributed Authoring and Versioning
= 공동 작업과 버저닝 관리에 대한 협업 관리 기술이다.

마찬가지로 HTTP를 확장하는 방식으로 구현되었는데, HTTP에 추가하는 메서드들을 살펴보면 아래와 같다.

- PROPFIND : 리소스의 속성을 읽음

- PROPPATCH : 하나 이상의 리소스에 대해 하나 이상의 속성 설정

- LOCK : 하나 이상의 리소스를 잠금

- UNLOCK : 하나 이상의 리소스를 잠금 해제


HTTP는 요청과 응답 정보를 헤더에 담아 보내게 되는데, 이는 요청 하나에 여러 개의 리소스가 존재할 때 사용하는 데에 있어 한계가 있다.

따라서 구조화(structured)된 데이터를 담을 때 사용하는 XML을 지원하는데, 주로 아래와 같은 용도로 사용된다.

- 데이터 처리 설명 포맷, 서버의 복잡한 응답을 다시 표현하는데 사용 등

# WebDav와 XML

WebDAV는 HTTP/1.1 프로토콜의 확장으로서 HTTP 및 XML 뿐만 아니라 텍스트, 그래픽, 스프레드시트 및 모든 기타 형식을 포함하는 모든 유형의 웹 리소스에 대해 저작 지원을 제공하는 새로운 HTML 메소드 및 헤더를 추가합니다.

WebDAV로 실행할 수 있는 작업에는 다음과 같은 것들이 있습니다.

등록정보(메타 데이터) 조작. WebDAV 메소드 PROPFIND 및 PROPPATCH를 사용하여 저작자 및 작성 날짜와 같은 웹 페이지에 대한 정보를 만들고 제거, 쿼리할 수 있습니다.
컬렉션 및 리소스 관리. WebDAV 메소드 GET, PUT, DELETE 및 MKCOL을 사용하여 문서 세트를 만들고 계층적 구성원 목록(파일 시스템의 디렉토리 목록과 유사)을 검색
잠금. WebDAV를 사용하여 한 사람 이상이 동시에 한 문서에서 작업하지 못하도록 할 수 있습니다. WebDAV 메소드 LOCK 및 UNLOCK을 사용하여 exclusive 또는 shared 잠금을 사용함으로써 "업데이트 유실"(변경 사항 겹쳐쓰기) 문제를 방지할 수 있습니다.

이름 공간 작업. WebDAV를 통해 WebDAV 메소드 COPY 및 MOVE를 사용하여 웹 리소스를 복사 및 이동하도록 서버에게 지시할 수 있습니다.

https://www.youtube.com/watch?v=lO22a85Bwx0

WebDAV의 메서드는 요청과 응답 관련 정보를 모두 잘 다루어야 한다. 하지만 헤더에만 정보를 담아 전송하는 것은 하나의 요청에 있는 여러 개의 리소스나 계층 관계에 있는 리소스들에 대한 정보를 헤더에 선택적으로 기술하기 어려운 점 등 한계가 있다.

WebDAV는 이 문제를 해결하려고 XML(Extensible Markup Language)을 지원한다. WebDAV는 XML을 다음과 같은 용도로 사용한다.

데이터를 어떻게 처리할 것인지 설명하는 명령 포맷
서버의 복잡한 응답을 표현하는 데 사용하는 포맷
콜렉션과 리소스를 처리하는 데 사용하는 커스텀 정보 포맷
데이터 자체를 표현할 수 있는 유연한 포맷


WebDAV는 현재 많은 브라우저에서 지원되고 있다고 한다.