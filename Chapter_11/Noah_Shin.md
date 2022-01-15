# Chap 11. 클라이언트 식별과 쿠키 
- 웹 서버는 서로 다른 수천개의 클라이언트와 동시에 통신한다
- 서버 들은 익명의 클라이언트로 부터 받는 모든 요청을 처리하는 것 뿐만 아니라 서버와 통신하고 있는 클라이언트를 추적해야 할 수도 있다

## 개별 접촉
- HTTP는 익명으로 사용하며 상태가 없고 요청과 응답으로 통신하는 프로토콜
 
- 웹 서버는 요청을 보낸 사용자를 식별 하고 사용자의 요청을 추적하기 위해 약간의 정보를 이용한다
 ex) 쇼핑몰이 사용자 맞춤 추천 , 불필요한 정보를 매번 입력하는것 방지  
 
- HTTP 트랜잭션은 상태가 없다 많은 웹사이트에서 사용자의 상태를 남겨 
  사용자와 사이트를 상호작용 시킨다  

## HTTP 헤더
### From 헤더 
  
  From 헤더는 사용자의 이메일 주소를 포함한다 -> From 헤더로 사용자를 식별할 수 있다  
  그러나 악의적으로 이메일 주소를 모아 스팸메일 보내는 경우가 있어 From 헤더를 보내는 브라우저는 많지 않다  
### User-Agent 헤더  

 User-Agent 헤더는 사용자가 쓰고 있는 브라우저의 이름과 버전, 어떤 경우에는 운영체제에 대한 정보까지 서버에 보낸다  
 그러나 특정 사용자를 식별하는데는 큰 도움이 되지 않는다  
### Referer 헤더  

  Referer 헤더는 현제 페이지로 유입하게 한 웹페이지의 URL을 가리킨다.  
  사용자가 이전에 어떤 페이지를 방문함을 알수 있어 사용자의 취향을 알 수 있다  
  그러나 사용자를 확실히 식별하기에는 다소 부족하다  
## 클라이언트 IP 주소
**초기에 웹 선구자들은 사용자 식별에 클라이언트의 IP 주소를 사용하려 했다.**

#### 문제점
- 클라이언트 IP 주소는 사용자가 아닌 사용하는 컴퓨터를 가리킨다 -> 사용자 식별 구별 불가
- 사용자가 로그인하면 동적으로 IP 주소를 할당하기 때문에 사용자는 매번 다른 주소를 받아 IP 주소로 식별 불가능하다
- 방화벽을 사용해 클라이언트의 실제 IP 주소가 아닌 하나의 방화벽 IP 주소로 변환한다.
- HTTP 프락시와 게이트 웨이는 원 서버에 새로운 TCP 연결을 한다
웹 서버는 클라이언트의 IP 주소가 아닌 프락시 서버의 IP 주소를 본다.


## 사용자 로그인
- 따라서 IP 주소로 사용자슬 식별하는 것보다 사용자에게 인증을 요구 해서 
  명시적으로 식별 요청을 할 수 있다.  
- 서버에서 사용자가 사이트가 접근하기 전에 로그인을 시키자고 한다면 HTTP 401 Login 
  Required 응답 코드를 브라우저에 보낸다  
- 다음 요청부터 Authorization 헤더에 그 정보를 기술하여 보낸다.


모두가 알다시피 웹사이트 로그인은 귀찮은 일이지, 개발시작하기 전까진 몰랐지... 어느 웹사이트나 회원가입 로그인은 존재했으니까...

사용자가 사이트를 옮겨 다닐때마다 로그인 해야한다. 또한 서로 다른 사용자 이름과 비밀번호를 기억해야 한다.

## 뚱뚱한 URL
- URL 경로의 처음과 끝에 어떤 상태 정보를 추가해 확장한다.  
- 사용자의 상태 정보를 포함하고 있는 URL을 뚱뚱한 URL 이라고 한다.  

#### 문제점
- 못생긴 URL은 사용자에게 혼란을 준다.
- 공유하지 못하는 URL -> URL을 공유하면 내 누적정보를 상대가 볼 수 있다.
- URL이 달라지기 때문에 기존 캐시에 접근할 수 없음
- 서버 부하 과중
- 의도치 않게 뚱뚱한 URL 세션에서 벗어날 확률이 높음
- 로그아웃하면 모든 정보를 잃음

## 쿠키
- 쿠키는 사용자를 식별하고 세션을 유지하는 방식 중 가장 널리 사용되는 방법  
- 쿠키는 매우 중요하고, 새로운 HTTP 헤더를 정의한다.  
- 대부분의 캐시나 브라우저는 쿠키에 있는 내용물을 캐싱하지 않는다.  

### 쿠키의 타입
_**세션 쿠키(Session Cookie)**_
- 사용자의 선호사항을 저장하는 임시 쿠키  
- 사용자가 브라우저를 닫으면 삭제 된다.  

_**지속 쿠키(persistent Cookie)**_
- 브라우저를 닫거나 PC를 재시작 하더라도 남아있다.  
- Expires혹은 Max-Age 파라미터가 없으면 세션 쿠키가 된다 -> 파기 되면 세션 쿠키가 된다.

### 쿠키는 어떻게 동작하는가?
- 쿠키는 서버가 사용자에게 '안녕 .. 내 이름은 ' 라고 적어서 붙이는 스티커와 같다.  
- 웹 서버는 사용자가 다시 돌아 왔을때 해당 사용자를 식별하기 위해 유일한 값을 쿠키에 할당한다.  
- Set-Cookie 혹은 Set-Cookie2 같은 HTTP 응답 헤더에 기술되어 사용자에게 전달한다.  

#### 쿠키 상자 : 클라이언트 측 상태
- 쿠키의 기본적인 발상은 브라우저가 서버 관련 정보를 저장하고 사용자가 해당 서버에 접근할때 
  그 정보를 함께 전송한다.  
  
  ![](https://images.velog.io/images/noahshin__11/post/d6148747-e7a6-4a36-b8c5-affc3c4e4255/image.png)

- 브라우저는 쿠키를 저장할 책임이 있다 = 이를 '클라이언트 측 상태' 라고 한다.  
- 구글 크롬 쿠키와 마이크로 소프트 인터넷 익스플로러 쿠키 등이 있다.  

### 사이트마다 각기 다른 쿠키들
- 쿠키 전부를 모든 사이트에 보내는 것이 아니라 보통 각 사이트에 두 개 혹은 세 개의 쿠키만을 보냄

#### 이유

1. 쿠키를 모두 전달하면 성능이 크게 저하된다.
2. 쿠키 대부분은 서버에 특화된 이름/값 쌍을 포함하고 있기 때문에, 대부분에 사이트에서는 인식하지 않는 무의미한 값
3. 모든 사이트에 쿠키를 전달하는 것은 잠재적인 개인정보 문제를 일으킨다.

- 브라우저는 쿠키를 생성한 서버에게만 쿠키에 담긴 정보를 전달한다.  
- ex) joes-hardware.com 에서 생성된 쿠키는 joes-hardware.com 에만 보낸다.  
- 쿠키 domain 속성  
  Set-cookie 응답 헤더에 Domain 속성을 기술한다.  
  
- Set-cookie : user="mary17"; domain = "airtravlebargains.com"
이는 user=mary17 라는 쿠키를 .airtravlebargains.com 도메인을 가진 모든 사이트에 전달함을 의미한다.  
- 쿠키 Path 속성  
Url 경로의 앞부분을 가리키는 Path 속성을 기술해서 해당 경로에 속하는 페이지에만 
쿠키를 전달한다. 

**따라서 쿠키는 일종의 상태 정보이며 서버가 생성하여 클라이언트에 전달하고 클라이언트는 그 쿠키를 유효한 사이트에만 다시 전달하고 관리한다**

### 쿠키와 세션 추적
- 쿠키는 웹 사이트에 수차례 트랜잭션을 만들어내는 사용자를 추적하는데 사용한다.

### 쿠키와 캐싱
- 쿠키 트랜잭션과 관련된 문서를 캐싱하는 것은 주의해야 한다.  
- 이전 사용자의 쿠키가 다른 사용자에게 할당되거나 누군가의 개인정보가 다른이에게 노출될 수 있다.  

1. 캐시되지 말아야 할 문서가 있다면 표시하라.
2. Set-Cookie 헤더를 캐시 하는 것에 유의하라.
3. Cookie 헤더를 가지고 있는 요청을 주의하라.

### 쿠키,보안 그리고 개인정보
- 쿠키를 사용하지 않도록 비활성화 할 수 있고 다른 방법으로 대체 가능하므로 그 자체가 보안상 엄청난 위험은 아니다.  
- 개인정보를 누가 받는지 알고 사이트의 개인정보 정책에 유의하면 쿠키에 대한 위험성보다 세션 조작이나 트랜잭션상의 편리함이 크다.