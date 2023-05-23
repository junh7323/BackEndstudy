# TECHIT 1주차 강의 기록 <br>Web의 동작 원리 - 클라이언트와 서버의 만남

브라우저를 통해 요청(request)을 보내는 주체 = 클라이언트

클라이언트의 요청을 수신하여 처리 후 응답(response)을 전달하는 주체 = 서버

### <br>http(HyperText Transfer Protocol)
>HyperText = 다른 리소스로 이동할 수 있는 장치

클라이언트와 서버는 http라는 일정한 규칙으로 서로 소통

## <br>URL(Uniform Resource Locator)
### URL 해체 분석기 <img src = "https://opgg-com-image.akamaized.net/attach/images/20200301074052.853300.jpg" width = "80" height = "80">

https://www.google.com/search?q=techit 를 예로 들어 본다면,

- https://

프로토콜 - 통신 규칙, HTTP(HTTPS), FTP 등

- www.google.com

호스트 - 서버의 주소, google.com을 호스트 네임이라고 지정

- /search

경로(Path) - 호스트 내 서비스의 위치, 서비스 별로 분할 ex) 검색, 회원 등

- ?q=techit

쿼리 문자열(Query String) - ?기호로 시작, &로 연결, 키/값 쌍으로 구성

## 쿠키
1. 서버에서 클라이언트로 보내져 브라우저에 저장되는 작은 크기의 데이터
2. 속성을 나타내는 키와 그 속성에 해당하는 값으로 구성
3. 유효기간이 만료되면 브라우저에서 삭제됨


http는 각각의 요청과 응답이 독립적, 이전의 작업을 기억하지 못함. 
>각각의 요청과 응답이 종료되었을 때 연결이 지속 x, 상태를 기억하지 않는다는 Stateless 라는 특성을 가지고 있음.

예를 들어, 로그인을 하고 장바구니로 이동하면 로그인을 했다는 데이터를 기억하지 못하기 때문에 데이터를 남겨 놓아야 함.

이를 해결하기 위해 쿠키에 정보를 저장함(쿠키 데이터)

## 세션

- 쿠키에서 보여지는 한계점, 단점들을 보완하기 위해 나온 개념 
- 클라이언트의 상태를 나타내는 쿠키 데이터들을 서버 측 세션 저장소에 가지고 있게 됨
- 클라이언트에서 불필요하게 많은 민감 정보와 같은 보안에 취약한 정보들을 갖고 있지 않아도 됨
- 세션은 민감한 쿠키 데이터들이 클라이언트에 저장되어 노출되는 것을 방지, 클라이언트가 매번 요청 시 쿠키 값을 보내는 리소스 비용을 절감한다는 장점

## 네트워크
#### 두 대 이상의 컴퓨터가 연결된 통신망을 의미

- 호스트(host)
  - 구성된 네트워크에서 연결된 개별 컴퓨터들
- 스위치(switch)
  - 많은 컴퓨터를 하나의 네트워크 망 안에 구성하기 위해 연결을 위한 매개체
  - 동일한 네트워크 내에서 호스트 간 통신을 가능하게 해주는 장비, 다른 네트워크는 접근 불가.
- 라우터(router)
  - 다른 네트워크 간 통신도 가능하게 하는 장비(공유기)

__인터넷 = 네트워크와 네트워크가 연결된 거대 통신망__

## IP(Internet Protocol)
- 컴퓨터 간 데이터를 주고받는 네트워크 계층의 규약
- 데이터 전달에 필요한 목적지 컴퓨터 정보가 필요

### ip 주소 = 네트워크에서 컴퓨터가 부여받는 고유한 주소
- ipv4 = 32bit
- ipv6 = 128bit

#### 공인ip (public ip)
- 전체 인터넷 망에서 고유하게 식별 가능한 주소
- ipv4 체계에서 자원 부족

#### 사설ip (private ip)
- 가정의 LAN과 같은 네트워크에서 할당되는 주소
- 컴퓨터에서 조회되는 ip

#### 127.0.0.1 (localhost)
- 컴퓨터 관점에서 자기 자신을 지칭하기 위해 약속된 아이피 주소
- 말 그대로 내 컴퓨터에서만 유효

## Port
- 하나의 컴퓨터에서 실행되고 있는 다양한 서비스를 구분하는 역할
- 접근하려는 서비스의 목적지 포트를 정확하게 설정해야 함

## DNS(Domain Name Server) 
- URL을 해석하여 IP 주소로 변환하는 서버

# TECHIT 2주차 강의 기록 <br>Django 구조 및 작동원리 & Django CRUD API 구현

## <br>1. DRF(Django REST Framework)란?
Django REST Framework는 장고 안에서 RESTful 한 API 서버를 쉽게 구축할 수 있도록 도와주는 오픈소스 라이브러리를 의미

API, REST API, RESTful의 정의

- API 
  - 응용프로그램 데이터를 주고받는 규약

- REST API 
  - Json 형태로 CRUD 데이터를 주고받는 규약

- RESTful
  - REST 방식을 따라서 개발하는 것

여기서 REST 방식이라고 한다면 자원과 이 자원에 대한 행위를 나눠서 작성하는 것을 말하며, 
<br>간단한 예제로는 유저에 대한 것을 예를 들면


GET /user      : 유저의 정보들을 가져옴

GET /user/1    : 1번 유저의 정보를 가져옴

PUT /user/1    : 1번 유저의 정보를 수정함

POST /user/1   : 1번 유저를 만듦

DELETE /user/1 : 1번 유저를 삭제함

 

등의 방식으로 표현 가능

### DRF의 큰 기능
- Models를 serializers로 변환하는 것
- 직렬화(serializer)를 하여서 메모리에 존재하고 추상적인 Object를 String or bytes로 만들어 드라이브에 저장 및 통신선 전송도 가능

### 직렬화(serializer)
모든 프로그래밍 언어의 통신에서 데이터는 필히 문자열로 표현되어야 함.

송신자 : 객체를 문자열로 변환하여 전송 -> 직렬화
<br>수신자 : 수신한 문자열을 다시 객체로 변환하여, 활용 -> 비직렬화


#### 장고와 DRF 차이
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbpZ59y%2FbtrBiZDTTlc%2Frn7ptKukKWWKzs8SC4Kic0%2Fimg.png">


#### 직렬화와 역직렬화 도식도
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZjzkn%2FbtrBi79K9ol%2FTU0Q7L1xFYVwY9oXkHH010%2Fimg.png">

DRF는 데이터 전송 중간에 직렬화를 시켜줌. 
>간단하게 한 줄로 된 긴 문자열로 만들어준다고 생각하면 되겠습니다. 
이것을 이용해서 데이터를 보내게 되며 받는 곳에서는 이 데이터 스트링과 그 데이터의 포맷 정보를 받아서 역직렬화 하여 Object로 다시 변경하여 사용하게 되는 것입니다.

### CORS(Cross-Origin Resource Sharing)
- 다른 출처의 자원을 공유. 교차 출처 리소스 공유 (Cross-origin Resource Sharing, Cors)는 추가 HTTP헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을부여하도록 브라우저에 알려주는 체제
#### 왜 필요한가?
- CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 된다면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 된다. 만약 기존 사이트와 완전히 동일하게 동작하도록 하여 사용
자가 로그인을 하도록 하고, 로그인했던 세션 또는 토큰을 탈취하여 악의적으로 정보를 꺼내오거나 다른 사용자의 정보를 입력하는 등 해킹을 할 수 있기에 보안상의 이유로 사용되고 있다.

### CRUD
-  CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말

##### 데이터베이스 SQL문과 대응
| 이름 | 조작 | SQL |
|---|---|---|
| Create | 생성 | INSERT |
| Read(또는 Retrieve) | 읽기(또는 인출) | SELECT |
| Update | 갱신 | UPDATE |
| Delete(또는 Destroy) | 삭제(또는 파괴) | DELETE |
