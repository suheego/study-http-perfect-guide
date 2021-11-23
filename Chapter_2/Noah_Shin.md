후... 수달 스터디 처음인데... 자 한번...

![](https://images.velog.io/images/noahshin__11/post/e428f373-342e-445b-af36-36eb21d41f1f/image.png)

# chapter. 2 

# 키워드

- ## URL 문법, 여러 URL 컴포넌트가 어떤 의미를 가지며 무엇을 수행하는지

- ## 여러 웹 클라이언트가 지원하는 상대 URL과 확장 URL 같은 단축 URL 에 대해서

- ## URL의 인코딩과문자규칙.

- ## 여러인터넷정보시스템에적용되는공통URL스킴.

- ## 기존 이름은 유지하면서 객체들을 다른 장소로 옮기는 것을 가능하게 해주는

                     URN(Uniform Resource Name)을 포함한 URL의 미래.
                     근데 이건 나중에 책 뒤에서 좀 더 알아보자

# Uniform Resource Identifier (URI)

# Uniform Resource Locator (URL)

=================================

http://www.joes-hardware.com/seasonal/index-fall.html

1. URL의 첫 부분인 http는 URL의 스킴이다. 스킴은 웹 클라이언트가 리소스에 어
떻게 접근하는지 알려준다. 이 경우에, URL이 HTTP 프로토콜을 사용한다.

• URL의 두 번째 부분인 www.joes-hardware.com은 서버의 위치다. 이는 웹 클라
이언트가 리소스가 어디에 호스팅 되어 있는지 알려준다.

• URL의 세 번째 부분인 /seasonal/index-fall.html은 리소스의 경로다. 경로는 서
버 에 존재하는 로컬 리소스들 중에서 요청받은 리소스가 무엇인지 알려준다.

![](https://images.velog.io/images/noahshin__11/post/c2760a71-cad6-460c-babf-c1e993ebc45d/image.png)


URL은 HTTP 프로토콜이 아닌 다른 가용한 프로토콜을 사용할 수도 있음
mailto:president@whitehouse.gov
는 이메일 주소를 가리키며,

ftp://ftp.lots-o-books.com/pub/complete-price-list.xls
는 FTP(File Transfer Protocol) 시버 에 올라가 있는 파일을 가리키고,

rtsp://www.joes-hardware.com:554/interview/cto_video
는 스트리밍을 제공하기 위해 비디오 서버에 호스팅하고 있는 영화를 가리킨다. 


이렇게 URL은 인터넷에 있는 어떤 리소스든지 가리킬 수 있다.


 대부분의 URL은 동 일하게 ‘스킴://서버위치/경로’ 구조로 이루어져 있다. 따라서 인터넷상의 모든 리 소스를 가리키고 가져오기 위해, 그리고 모든 사람이 같은 방식으로 이름을 써서 리소스를 찾을 수 있도록, 단일 방식의 작명 규칙을 가진 것이다. 하지만 처음부터 일관된 명명 방식이 있었던 것은 아니다.
 
 # 라떼는 마리야...~ 
 
 
 ftp://ftp.lots-o-books.com 일로가
 /pub 일로가
 /complete-catalog.xls 열어
 
 이런식으로 막 단계를 나눠서 여러번 했다 ~ 이 마리야 ~
 
 지금은 
 ftp://ftp.lots-o-books.com/pub/complete-catalog.xls
 요즘 애들은 너무 온실 속의 화초처럼 자랐어 ~
 
 ## URL은 당신과 브라우저에게 정보 찾는데 필요한 모든 것을 제공하며, 당신이 원하는 리소스가 어디에 위치하고 어떻게 가져오는지 정의한다.
 
 =================================
 진짜 빡세게 하면 
 <스킴>://<사용자 이름>: <비밀번호>@<호스트>: <포트>/<경로>;<파라미터>?<질의>#<프래그먼트>
 
 근데 제일 중요한건 
 - 스킴
 - 호스트
 - 경로
 
 ![](https://images.velog.io/images/noahshin__11/post/dcc7bca6-3969-4d3b-8539-143a08f825f0/image.png)
 
 
 =================
 ## 스킴
 
 스킴 컴포넌트는 알파벳으로 시작해야 하고 URL의 나머지 부분들과 첫 번째 ‘:’ 문자로 구분한다. 
 
>  스킴 명은 **_대소문자를 가리지 않으므로_** ‘http://www.joes-hardware.com’와 ‘HTTP://www.joes-hardware.com’는 같다.
 
 
 ## 호스트와 포트
 
 애플리케이션이 인터넷에 있는 리소스를 찾으려면, 리소스를 호스팅하고 있는 장 비와 그 장비 내에서 리소스에 접근할 수 있는 서버가 어디에 있는지 알아야 한다. 

### URL의 호스트와 포트 컴포넌트는 그 두 가지 정보를 제공해준다.
 - http://www.joes-hardware•com:80/index.html
 - http://161.58.228.45:80/index.html
 
 둘이 같은겨
 포트 컴포넌트는 서버가 열어놓은 네트워크 포트를 가리킨다. 
 내부적으로 TCP 프 로토콜을 사용하는 HTTP는 기본 포트로 80을 사용한다.
 
 ## 사용자 이름과 비밀번호
 더 흥미로운 컴포넌트는 사용자 이름과 비밀번호 컴포넌트다. 
 많은 서버가 자신이 가지고 있는 데이터에 접근을 허용하기 전에 사용자 이름과 비밀번호를 요구한다. 
 FTP 서버가 좋은 예다. 
- ftp://ftp.prep.ai.mit.edu/pub/gnu
- ftp://anonymous@ftp.prep.ai.mit.edu/pub/gnu
- ftp://anonymous:my_passwd@ftp•prep.ai.mit•edu/pub/gnu
- http://joe:j oespasswd@www.joes-ha rdwa re•com/sales_info.txt


첫 번째 예는 사용자 이름이나 비밀번호 컴포넌트가 없이 표준 스킴, 호스트, 경로만 있다.
애플리케이션이 FTP와 같이 사용자 이름과 비밀번호를 요구하는 URL 스킴을 사용한다면, 그 값들이 삽입되어 있지 않을 경우 기본 사용자 이름과 비밀 번호 값을 넣어놓을 것이다. 
예를 들어, 사용자 이름과 비밀번호를 기술하지 않고 FTP URL에 접근하면, 기본 사용자 이름 값으로 ‘anonymous’가, 비밀번호는 브라 우저마다 가지고 있는 기본값을 사용한다
(인터넷 익스플로러는 ‘lEUser’를, 크롬은 ‘chrome@example.com’을 넣는다).

두 번째 예에는 사용자 이름이 ‘anonymous’로 되어 있다. 
호스트 컴포넌트와 나란히 기술되어 있는 사용자 이름은 단순한 이메일 주소처럼 보이기도 한다. 
문자는 URL로부터 사용자 이름과 비 밀번호 컴포넌트를 분리한다.

세 번째 예는 사용자 이름(‘anonymous’)과 비밀번호(‘my_passwd’)를 문자로 분리하여 모두 기술하였다.

## 경로

경로는 서버가 리소스의 위치를 찾는데 사용하는 정보다.
HTTP URL에 서 경로 컴포넌트는 ‘/’문자를 기준으로 경로조각으로 나뉜다(다시 한번 말하지만, 유닉스 파일 시스템의 파일 경로와 유사하게). 

## 파라미터

많은 스킴이 객체에 대한 호스트 및 경로 정보만으로는 리소스를 찾지 못한다. 
서버가 어떤 포트를 열어놓고 있는지, 리소스에 접근하기 위해 사용자 이름과 비밀번호를 명시했는지 여부 외에도 많은 프로토콜이 더 많은 정보를 요구한다.

### 질의 문자열

다음 URL은 아이템 번호 12731의 재고 가 있는지 확인하기 위해서 웹 데이터베이스 게이트웨이에 질의하는데 사용된다.
http://ww.joes—hardware.com/inventory—check.cgi?item=12731
노아: 헐? 

![](https://images.velog.io/images/noahshin__11/post/fa0412b9-cdab-482c-842a-a29e62622f6a/image.png)

http://www.joes—hardware.com/inventory—check.cgi?item=12731&color=blue

이 예에는 이름/값 쌍으로 된 두 개의 질의 컴포넌트가 존재한다. item=12731과 color=blue.

## 상대 URL

URL은 상대 URL과 절대 URL 두 가지로 나뉜다. 지금까지 우리가 본 것들은 절대 URL뿐이었다. 절대 URL은 리소스에 접근하는데 필요한 모든 정보를 가지고 있다.

자 이게 URL 의 로직 다이어그램이라고 보면 될 것 같다.

![](https://images.velog.io/images/noahshin__11/post/00678687-074b-460a-9242-0c3f50c40412/image.png)


## URL 확장

검색창에 url 타이핑 할때 자동완성 말하는 거

호스트명 확장 & 히스토리 확장이 있다.


# 안전하지 않은 문자

URL은 잘 호환되도록 설계되었다. 
그리고 URL은 인터넷에 있는 모든 리소스가 여러 프로토콜을 통해서 전달될 수 있도록, 각 리소스에 유일한 이름을 지을 수 있게 설계되었다.
모든 프로토콜이 데이터를 전송하기 위해서 서로 다른 장치를 가지고 있기 때문에, 어떤 인터넷 프로토콜을 통해서든 안전하게 전송될 수 있도록 URL을 설계하는 것은 중요했다.



전자메일에 사용되는 SMTP(Simple Mail Transfer Protocol)같은 프로토콜은 특정 문자를 제거할 수도 있는 전송 방식을 사용한다.
문자가 제거되는 일을 피하고자 URL은 상대적으로 작고 일반적으로 안전한 알파벳 문자만 포함하도록 허락한다.

## URL 문자 집합


![](https://images.velog.io/images/noahshin__11/post/2f3c9c4c-71da-4240-9a01-05b3818d15e6/image.png)
노아: 이거 때문에 고생했었음

## 문자 제한

몇몇 문자는 URL 내에서 특별한 의미로 예약되어 있다. 

어떤 문자는 US-ASCII의 출력 가능한 문자 집합에 포함되어 있지 않다.

URL에서 예약된 문자들을 본래의 목적이 아닌 다른 용도로 사용하려면, 그 전에 반드시 인코딩해야 하는 문자들을 나열해 놓았다.
![](https://images.velog.io/images/noahshin__11/post/e020c2ad-c052-4f99-a873-3554029715f4/image.png)
![](https://images.velog.io/images/noahshin__11/post/8dec5171-9a99-4c36-a836-dbda4a9c1e47/image.png)

입력받은 URL에서 어떤 문자를 인코딩해야 하는지 결정하는 데는 브라우저와 같 이 사용자로부터 최초로 URL을 입력받는 애플리케이션에서 하는 것이 가장 적절 하다.

URL을 구성하는 각 컴포넌트마다 사용할 수 있거나 없는 문자들이 있을 것이 고, 또 어떤 문자는 스킴에 따라서 가용성이 달라지기 때문에, 해당 문자들을 직접 입력 받는 애플리케이션이야말로 어떤 문자를 인코딩해야 하는지 결정하기에 가장 좋은 위치라는 것이다.

물론 극단적인 방법은 애플리케이션이 모든 문자를 인코딩하는 것이다.

이 방식 을 추천하지는 않지만, 이미 안전한 것으로 판단되는 문자를 재차 인코딩하는 것보
다 더 완벽하고 빠른 규칙은 없다. 하지만 실제로 이 방식은 안전한 문자들을 인코 딩하지 않는 애플리케이션도 있기 때문에 오동작을 일으킬 수 있다.

## 스킴의 바다
 웹에서 쓰이는 일반 스킴들의 포맷에 대해 알아볼 것이다. 
![](https://images.velog.io/images/noahshin__11/post/42d03514-61e2-4fe5-a10c-fa20d3c94571/image.png)


![](https://images.velog.io/images/noahshin__11/post/0735d101-5df7-4551-9b31-7f902089f5a3/image.png)

![](https://images.velog.io/images/noahshin__11/post/055841f0-1f8d-4752-9ed0-13decd6adaff/image.png)

## 미래


URL은 나름의 한계를 가지고 있지만, 웹 개발 커뮤니티에
서 이를 가장 긴급한 사안이라고 이야기하지는 않는다.

URL에서 URN으로 주소 체계를 바꾸는 것은 매우 큰 작업이다. 표준화는 매우 중 요한 작업인 만큼 느리게 진행될 때도 있다. URN을 지원하려면 많은 변화가 필요 할 것이다. 표준을 제정하는 것에서부터 여러 HTTP 애플리케이션을 수정하기 위 한 벤더들과의 합의도 필요하다.

노아: 수많은 링크들을.. 언제 다 바꿔...

 URL은 그 한계를 가진 상태에서, 그것을 해결할 수 있는 새로운 표준(아마도 URN) 같은 것들이 나오고 적용될 것이다.