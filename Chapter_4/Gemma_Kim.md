# 4장 : 커넥션 관리

## TCP 커넥션

- HTTP는 전송계층인 TCP 커넥션을 통해 인터넷을 연결
- 커넥션의 클라이언트 측에 있는 바이트들을 서버로 순서대로 전달해 **안전하게** 인터넷을 연결 시킴

> **TCP 스트림은 세그먼트로 나뉘어 IP 패킷을 통해 전송**

- 세그먼트라는 단위로 데이터 스트림을 잘게 나누어 IP 패킷에 담아 데이터를 전달
- 각 TCP 세그먼트는 하나의 IP 주소에서 다른 IP 주소로 IP 패킷에 담겨 전달됨
- IP 헤더는 발신지와 목적지 IP 주소, 크기, 기타 플래그를 가짐

> **TCP 커넥션 유지**

- 컴퓨터는 항상 TCP 커넥션을 여러 개 가짐
- TCP 포트 번호를 통해 여러 개의 커넥션을 유지
- TCP 커넥션은 < **_발신지 IP 주소, 발신지 포트, 수신지 IP 주소, 수신지 포트_** > 네 가지로 이루어짐

> **TCP 소켓 프로그래밍**

![소켓 프로그래밍.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/216cbddd-8a20-4477-a171-e384f2006b53/%E1%84%89%E1%85%A9%E1%84%8F%E1%85%A6%E1%86%BA_%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC.png)

- 소켓 (Socket) ?
  - 데이터를 보내거나 받는 역할 따라 서버 소켓인지 클라이언트 소켓인지 구분
  - 네트워크를 통해 서로 통신을 수행할 수 있도록 양쪽(클라이언트, 서버)에 생성되는 링크의 단자
  - 두 소켓이 연결되며 서로 다른 프로세스가 데이터를 전달할 수 있음
- TCP 소켓 API
  - 소켓 API를 사용해 데이터 구조를 생성
  - 원격 서버의 TCP 종단에 그 종단 데이터 구조를 연결하여 데이터 스트림을 읽고 씀

## TCP의 성능 최적화

<aside> 🗣 **TCP 프로토콜에 관한 기본적 이해가 더 좋은 성능의 HTTP 애플리케이션을 설계할 수 있도록 한다 !**

</aside>

> **HTTP 트랜잭션 지연 원인**

- 하드웨어의 성능
- 네트워크와 서버의 전송 속도
- 요청과 응답 메시지의 크기
- 클라이언트와 서버 간의 거리

> **TCP** **성능 관련 중요 요소**

1. TCP 커넥션 핸드셰이크 설정

   1. TCP 커넥션 생성 위해 작은 TCP 패킷을 서버에 보냄

      ⇒ 'SYN' 플래그 ( 생성 요청 )

   2. 서버가 그 커넥션을 받으면 요청이 받아들여졌음을 의미하는 TCP 패킷을 클라이언트에 보냄

      ⇒ 'SYN' + 'ACK' ( 커넥션 요청 허용 )

   3. 확인응답 신호

   4. 실제로 이 패킷들을 확인 X ⇒ 핸드셰이크 지연 발생

2. TCP 의 느린 시작(slow-start)

   1. 부하와 혼잡을 제어하기 위함
   2. TCP 데이터 전송 속도는 커넥션이 만들어진 지 얼마나 지났는 지에 따라 다름

3. 네이글(nagle) 알고리즘과 TCP_NODELAY

   1. 많고 작은 패킷들을 전송한다면 네트워크 성능이 크게 떨어짐
   2. 패킷을 전송하기 전 많은 양의 데이터를 한 데 모아 한 번에 전송

4. 확인응답 지연 알고리즘

   1. 데이터 패킷에 같은 방향으로 가는 확인 응답을 편승 시켜 네트워크 효율성 상승
   2. HTTP 동작 방식은 요청, 응답 두 가지 형식이라 송출 데이터 패킷에 편승할 기회 감소

5. TIME_WAIT 지연과 포트 고갈

   1. 커넥션이 끊긴 경우, 종단에서 커넥션의 IP 주소와 포트 번호를 메모리의 작은 제어영역에 기록
   2. 같은 주소와 포트 번호를 사용해 패킷은 중복되고 TCP 데이터가 충돌되는 것을 방지해 네트워크 성능이 떨지지 않도록 제어

## 병렬 커넥션

- **여러 개의 TCP 커넥션**을 통한 동시 HTTP 요청

> **더 빠르게 페이지를 내려 받음**

- 단일 커넥션의 대역폭 제한과 커넥션이 동작하고 있지 않은 시간 활용

> **병렬 커넥션이 항상 더 빠르지는 않다**

- 클라이언트의 네트워크 대역폭이 좁을 때 대부분의 시간을 데이터를 전송하는 데에만 사용
- 메모리를 많이 소모, 자체적인 성능 문제를 발생
- 과도한 커넥션이 맺어질 경우, 그것을 임의로 끊을 수 있음

> **병렬 커넥션은 더 빠르게 '느껴질 수' 있다**

- 시간이 더 소요되더라도 여러 작업이 화면에서 일어나고 있음을 **눈으로 확인**하는 것이 더 빠르다 느껴짐

## 지속 커넥션

- 커넥션을 맺고 끊는 데서 발생하는 지연을 제거하기 위한 **TCP커넥션의 재활용**
- HTTP/1.1 을 지원하는 기기는 처리가 완료된 후에도 커넥션을 유지하여 HTTP 요청에 재사용
- 비지속 커넥션은 각 처리가 끝날 때마다 커넥션을 끊지만, 지속 커넥션은 클라이언트나 서버가 끊기 전까지 트랜잭션 간에도 커넥션을 유지함
- 커넥션을 맺기 위한 준비작업에 따르는 시간을 절약

> **지속 커넥션 VS 병렬 커넥션**

- 병렬 커넥션의 장점
  - 네트워크 대역폭을 잘 활용하면 여러 객체가 있는 페이지를 더 빠르게 전송
- 병렬 커넥션의 단점
  - 각 트랜잭션마다 새로운 커넥션을 맺고 끊기에 시간과 대역폭이 소요
  - 가각의 새로운 커넥션은 TCP 느린 시작 때문에 성능이 떨어짐
  - 실제로 연결 가능한 병렬 커넥션의 수는 제한이 있다
- 지속 커넥션의 단점
  - 커넥션 관리를 잘못할 경우, 계속 연결된 상태로 있는 수많은 커넥션이 쌓이게 됨
  - 이는 로컬의 리소스, 우러결의 클라이언트와 서버의 리소스에 불필요한 소모를 발생
- 지속 커넥션의 장점
  - 커넥션을 맺기 위한 사전 작업과 지연을 줄여주고, 튜닝된 커넥션을 유지하며 커넥션의 수를 줄임

⇒ 지속 커넥션은 병렬 커넥션과 함께 사용될 때에 가장 효과적이다. HTTP/1.0+에는 'keep-alive', HTTP/1.1 에는 지속 커넥션이 있다.

> **Keep-Alive 커넥션**

- 기본으로 사용되지 않음
- 클라이언트는 Connection: Keep-Alive 요청 헤더를 보내야 함
- 서버 또한 계속 커넥션이 연결될 것이라면 Connection: Keep-Alive 요청 헤더를 응답에 담아 보내야 함
- 때론 멍청한(Dumb) 프락시와 함께 Keep-Alive를 사용될 땐 주의해야 한다.
- Proxy-Connection이라는 헤더를 사용하여 무조건적인 헤더 전달을 방지할 수 있다.
  - Proxy-Connection이라는 헤더는 영리한 프락시가 keep-alive 를 요청한다는 것을 인식해 자동으로 Connection: Keep-Alive 요청 헤더를 자체적으로 웹 서버에 전달

> **HTTP/1.1의 지속 커넥션**

- 클라이언트가 요청에 Connection: Keep-Alive 헤더를 담아보냈으면, 클라이언트는 그 커넥션으로 추가적인 요청을 보낼 수 없다.
- 커넥션에 있는 모든 메시지가 자신의 길이 정보를 정확히 가지고 있을 때에만 커넥션 지속
- HTTP/1.1 애플리케이션**은** 중간에 끊어지는 커넥션을 복구할 수 있어야 한다.
- 전체 응답을 받기 전 커넥션이 끊어지면, 요청을 반복해서 보내도 문제 없는 경우, 요청을 다시 보낼 준비가 되어야 한다
- 서버의 과부하를 방지하기 위해, 넉넉잡아 두 개의 지속 커넥션만을 유지.

## 파이프라인 커넥션

![파이프라인.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7032f77b-3317-4055-a868-e4948f900c64/%E1%84%91%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%91%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB.png)

- HTTP/1.1은 지속 커넥션을 통해서 요청을 파이프라이닝
- 응답은 요청 순서대로 와야함.
- 커넥션이 언제 끊어지더라도, 완료되지 않은 요청이 파이프라인에 있으면 언제든 다시 요청을 보낼 준비
- POST 요청 같이 비멱등성 요청을 재차 보낼 경우 문제가 생기는 요청은 파이프라인을 통해 보내선 안된다
  - 어떤 것들이 서버에서 처리 됐는지 알 길이 없다

> **커넥션 끊기**

- 커넥션은 언제든지 마음대로 끊을 수 있다
- 커넥션이 끊기더라도 언제든 다시 커넥션을 다시 맺고 요청을 전송을 시도해야한다.
  - 파이프라인 커넥션에서는 좀 더 어려운 문제다
  - 클라이언트는 여러 요청을 큐에 쌓아 놓을 수 있지만 서버는 아직 처리되지 않고 스케줄이 조정되어야 하는 요청을 남겨둔 채로 커넥션을 끊어 버릴 수 있다.
  - 이로 인한 부작용을 주의하여 비멱등 요청에는 파이프라인 커넥션을 맺어선 안된다.

> **우아하게 커넥션 끊기**

- 단순한 HTTP 애플리케이션을 전체 끊기만을 사용할 수 있다.
- 서버 출력 절반 끊기로 우아하게 커넥션을 끊을 수 있다.
  - 커넥션 반대편에 있는 기기는 데이터 전송이 안전하게 끝남과 동시에 커넥션을 끊었다는 것을 알게됨
- 클라이언트에서 더는 데이터를 보내지 않을 것임을 확실할 수 없는 이상, 커넥션의 입력 채널을 끊는 것은 위험
  - 이미 끊긴 입력 채널에 데이터를 전송하면 서버의 운영체제는 TCP 'connecton reset by peer' 메시지를 클라이언트에 보냄
  - 이는 대부분의 운영체재는 이것을 심각한 에러로 취급하여 버퍼에 저장된 데이터를 모두 삭제
- 우아하게 커넥션을 끊는다 하더라도 이를 안전하게 구현했는지 알 길이 없다
  - 출력 채널에 절반 끊기를 하고 난 후에 데이터나 스트림의 끝을 식별하기 위해 입력 채널에 대해 상태 검사를 주기적으로 해야한다

**참고 자료**

- https://recipes4dev.tistory.com/153

- https://juyoung-1008.tistory.com/19

- https://mygumi.tistory.com/141
