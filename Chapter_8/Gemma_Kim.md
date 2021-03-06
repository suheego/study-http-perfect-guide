# 8장 : 통합점: 게이트웨이, 터널, 릴레이

## 게이트웨이

![게이트웨이2.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62c4acbb-4229-4740-83ca-0c1ccabb6b27/%E1%84%80%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%B3%E1%84%8B%E1%85%B0%E1%84%8B%E1%85%B52.jpeg)

- 컴퓨터 네트워크에서 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 컴퓨터나 소프트웨어를 두루 일컫는 용어, 즉 다른 네트워크로 들어가는 입구 역할을 하는 네트워크 포인트
- 넓은 의미로는 종류가 다른 네트워크 간의 통로의 역할을 하는 장치. 또한 게이트웨이를 지날 때마다 트래픽(traffic)도 증가하기 때문에 속도가 느려질 수 있다.
- 목적지 서버를 **중계**한다는 점에선 프록시와 비슷하게 느껴질 수 있으나 네트워크 캐싱, 특정 웹 사이트 엑세스 방지, 엑세스 로그의 기능을 하는 프록시와 달리 서버와 HTTP 이외의 타 프로토콜과의 네트워크 통신을 가능하게 한다는 점에서는 다른 개념으로 볼 수 있다.

### 프로토콜 게이트웨이

- 게이트웨이는 리소스를 받기 위한 **경로**를 안내
- 한 쪽에서는 http 프로토콜을 사용하고 다른 한 쪽에서는 다른 타 프로토콜을 사용
- 웹 게이트웨이는 클라이언트 측 프로토콜과 서버 측 프로토콜을 (/) 으로 구별하여 기술

<aside> 📖 <클라이언트 프로토콜>/<서버 프로토콜> 게이트웨이

</aside>

1. HTTP/\*: 서버 측 웹 게이트웨이
   1. 서버 측 웹 게이트웨이는 클라이언트로부터 HTTP 요청이 원 서버 영역으로 들어오는 시점에 클라이언트 측의 HTTP 요청을 외래 프로토콜로 전환
2. HTTP/HTTPS: 서버 측 보안 게이트웨이
   1. 기업 내부의 **모든 웹 요청을 암호화**함으로써 개인 정보 보호, 보안을 제공하는데 게이트웨이를 사용할 수 있다. 클라이언트는 일반 HTTP를 사용하여 웹을 탐색할 수 있지만, 게이트웨이는 자동으로 사용자의 모든 세션을 암호화
3. HTTPS/HTTP: 클라이언트 측 보안 가속 게이트웨이
   1. 웹 서버의 앞단에 위치하고, 보이지 않는 인터셉트 게이트웨이나 리버스 프락시 역할
   2. 보안 HTTPS 트래픽을 받아서 복호화하고, 웹 서버로 보낼 일반 HTTP 요청을 생성
   3. 게이트웨이와 원 서버 간에 있는 암호화 하지 않은 트래픽이 존재하기에 **안전한지 확인**을 확실히 하고 사용할 것

### 리소스 게이트웨이

<aside> 📖 웹 서버가 애플리케이션과 연결되는 수단으로 사용되는 리소스 게이트웨이

</aside>

![게이트웨이3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/772b8908-701f-40c4-a18f-61f27d6331a9/%E1%84%80%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%B3%E1%84%8B%E1%85%B0%E1%84%8B%E1%85%B53.png)

- 게이트웨이의 가장 일반적 형태
- 애플리케이션 서버는 목적지 서버와 게이트웨이를 한 개의 서버로 결합

1. 공용 게이트웨이 인터페이스
   1. 가장 유명한 최초의 API는 공용 게이트웨이 인터페이스 (Common /Gateway Interface, CGI) 특정 URL에 대한 HTTP 요청에 따라 프로그램을 실행하고, 출력을 수집, HTTP 응답으로 회신하는데 웹 서버가 사용하는 표준화된 인터페이스 집합
2. 서버 확장 API

## 터널

<aside> 📖 웹 터널은 HTTP 프로토콜을 지원하지 않는 애플리케이션에 HTTP 애플리케이션을 사용해 접근하는 방법을 제공

</aside>

### HTTP 터널링 과정

- HTTP 메서드 CONNECT로 요청 전송
- 443 포트로 TCP 커넥션을 염
- HTTP 커넥션 준비 메시지 반환 - 200 OK

### SSL 터널링

- 웹 터널의 본 목적은 방화벽을 통해 암호화된 SSL 트래픽을 전달하기 위함
- 낡은 방식의 프락시에서는 방화벽을 뚫지 못해 통신 불가능
- 방화벽을 뚫는 유용한 방식이 아닌 악의적 트래픽이 유입될 가능성 존재

### 터널 인증

- 프락시 인증 기능을 통해 터널 커넥션을 허용할 수 있는 트래픽인지 권한 검사함
- 터널의 오용을 최소화 하기 위해 게이트웨이는 전용 포트인 443 같이 잘 알려진 특정 포트만을 터널링 하도록 하는 방식을 사용

## 릴레이

- HTTP 명세를 완전히 준수하지는 않는 간단한 HTTP 프락시
- 릴레이는 커넥션을 맺기 위한 HTTP 통신을 한 다음, 바이트를 맹목적으로 전달
- HTTP를 제대로 준수하는 프락시를 사용하는 것을 추천

**참고자료**

- https://it.donga.com/6744/

- https://tigger.dev/entry/network-gateway-tunnel-relay
