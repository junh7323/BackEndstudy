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


# TECHIT 3주차 강의 기록 <br>Prologue: 백엔드 개발 기초
## 웹 동작의 흐름
<br>사용자 > 브라우저 > 서버 > 데이터베이스
- 브라우저
  - 사용자에게 입력 제공, 데이터 출력과 같은 UI의 역할을 함
- 서버
  - 브라우저에게 받은 요청을 처리 및 응답하는 역할을 함
  - 비즈니스 로직, 연산 수행
  - 데이터베이스 관리
  
  
클라이언트와 서버는 '역할'이며 요청을 보내면 클라이언트, 요청을 응답하면 서버의 역할을 한다고 함

### 프론트엔드, 백엔드 비교
<br>프론트엔드
- 역할
  - 사용자 인터페이스
  - 사용자 입력
  - 데이터 출력
- 주요 기술
  - html, css, js, react, vue.js  
<br>백엔드
- 역할 
  - 시스템 관리 및 제어
  - 비즈니스 로직, 연산 수행
  - 데이터베이스 관리
- 주요 기술
  - python, java, C#, django, ubuntu, SQLite, oracle 등
## 웹 프레임워크
프레임워크(Framework)
- 소프트웨어 개발을 위한 기능, 구조의 틀 제공
- 시스템 흐름을 프레임워크가 제어함


라이브러리(Library)
- 소프트웨어 개발을 위한 기능 제공
- 시스템 흐름을 개발자가 제어함


### 프레임워크의 장점?
효율적 - 이미 구현되어 있는 코드로 시간과 비용을 절약, 생산성이 높음
품질향상 - 수많은 개발자들이 검증한 코드로 버그를 최소화 할 수 있음
유지보수 용이 - 체계적인 코드관리로 유지보수 용이/개발자 기준보다 프레임워크 기준으로 개발하기에 수월한 협업이 가능

### 단점
프로그래밍 언어 외 별도 학습 필요
<br>기본 설계된 구조로 개발이 다소 제한적

>프레임워크는 개발에 필수 존재


#### Django를 사용하는 이유
- 개발 속도가 상당히 빠름
- 기본적으로 필요한 기능을 제공
- 인증, 보안 부분들도 고려됨
- 풀스택 프레임워크

#### Django의 특징
- Python 웹 프레임워크
- MTV 디자인 패턴
- 오픈 소스
- 앱 단위로 프로젝트 구성

MTV 디자인 패턴
- Model(models.py)
 - 데이터 관리
 - 데이터 베이스와 연결 및 실행
- Template(html)
  - 데이터 출력
  - 사용자에게 표현 방식 정의 
- View(views.py)
  - 컨트롤러
  - 비즈니스 로직을 처리 
 
장고 실행 흐름
<br>웹 브라우저 > urls.py > view > model > view > template > view > 웹 브라우저

# TECHIT 4주차 강의 기록 <br>Chapter 2. 데이터베이스와 ORM 완벽 이해하기

## DataBase
- 공유의 목적으로 통합 관리되는 자료의 집합
- 논리적으로 연관된 하나 이상의 자료의 모음으로 내용을 구조화하여 검색과 갱신의 효율화한 것
- 중복을 없애고 자료를 구조화 하여 기억시켜 놓은 자료의 집합체

###  특징
- 실시간 접근성 - 사용자의 요구를 즉시 처리할 수 있다.
- 지속적인 변화 - 정확한 값을 유지하려고 삽입, 삭제, 수정 작업 등을 이용해 데이터를 지속적으로 갱신할 수 있다.
- 동시 공유 - 사용자마다 서로 다른 목적으로 사용하므로 동시에 여러 사람이 동일한 데이터에 접근하고 이용할 수 있다.
- 내용에 대한 참조 - 저장한 데이터 레코드의 위치나 주소가 아닌 사용자가 요구하는 데이터의 내용, 즉 데이터 값에 따라 참조할 수 있어야 한다.

## 데이터베이스 관리 시스템(DBMS) Management System
- 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어
- 사용자 또는 다른 프로그램의 요구를 처리하고 응답하여 데이터를 사용할 수 있도록 함
- 일반적으로 DB라고도 부름

### DBMS 장단점
- 장점
  - 데이터 중복 최소화
  - 데이터 독립성이 확보
  - 데이터를 동시 공유
  - 데이터 보안이 향상
  - 데이터 무결성이 유지
  - 장애 발생 시 회복이 가능

- 단점
  - 비용이 많이 발생
  - 백업과 회복 방법이 복잡
  - 중앙 집중 관리로 인한 취약점이 존재

### DBMS의 기능
- 정의 - 모든 응용 프로그램들이 요구하는 데이터 구조를 지원하기 위해 데이터베이스에 저장될 데이터의 형(type)과 구조에 대한 정의, 이용 방식, 제약 조건 등을 명시하는 기능이다.
- 조작 - 데이터 검색, 갱신, 삽입, 삭제 등을 체계적으로 처리하기 위해 사용자와 데이터베이스 사이의 인터페이스 수단을 제공하는 기능이다.
- 제어 - 데이터베이스를 접근하는 갱신, 삽입, 삭제 작업이 정확하게 수행되어 데이터의 무결성이 유지되도록 제어해야 한다.

### 테이블(table)
데이터베이스의 생긴 형태

### 구조적 질의 언어
- DDL, DML, DCL

## 객체와 데이터베이스의 데이터를 연결해주는 매체 = ORM
- object relational mapping (객체-관계 매핑)

- 장점
  - 생산성 향상, 비즈니스 로직 집중
  - 재사용 및 유지보수 용이
  - DBMS 종속되지 않음

- 단점
  - 프로젝트가 복잡한 경우 난이도 상승
  - Raw Query 보다 성능이 낮음

## MTV 디자인 패턴(Model, Template, View)

- Model
  - 데이터를 관리하는 역할
  - 데이터베이스에 저장할 테이블 정의
  - 모델에 작성된 코드를 기준으로 데이터베이스 생성(ORM)
  - 데이터베이스와 연결 및 실행

# TECHIT 5주차 강의 기록 <br>Chapter 3. QuerySet API와 Admin 개발하기

## QuerySet API
- Query: DB에 정보를 요청하는 것
- QuerySet: DB에서 전달 받은 객체의 목록
- QuerySet API: DB에 요청하기 위한 인터페이스

### Queryset API 주요 함수
- 새 QuerySet을 반환하는 메서드
	- filter()
	- exclude()
	- order_by()
	- select_related()
	- prefetch_related()
	- raw()

- Querysets를 반환하지 않는 메서드
  - get()
  - create()
  - count()
  - first()
  - last()

    
## Django shell
- 파이썬 인터프리터 형식으로 장고 사용
- Model을 import하여 사용 가능
- python manage.py shell

## Database Tool
- 데이터베이스의 관리를 위한 도구
- 툴을 활용하여 테이블이나 데이터를 조작
- GUI(Graphical User Interface) 제공

## Django는 기본적으로 관리자(admin) 인터페이스를 제공

settings.py 하단의 language code를 ko-kr로 수정하여 한글 설정이 가능

python mange.py createsuperuer - 어드민 계정 생성
python manage.py runserver - 서버 실행

http://127.0.0.1:8000/admin 을 통해 관리자 로그인 페이지로 이동 후 어드민 계정으로 로그인

posts - admin.py의 경로로 이동

from .models import, Comment > 관리자 페이지에 모델 등록 (Post, Comment를 import)
admin.site.register(Post)
admin.site.register(Comment)


# TECHIT 6주차 강의 기록 <br>Chapter 4. Template과 View 정복하기

## Views를 만드는 방법
### FBV(Function Based Views): 함수 기반 뷰 
- 장점
  - 구현이 간편함
  - 읽기 쉬우며 직관적인 코드
  - 데코레이터의 간단한 사용법
- 단점
  - 코드 확장과 재사용이 어려움
  - 조건부 분기를 통한 HTTP 메서드 처리
    
>일회성, 특수 목적이 있는 View에 적합

### CBV(Class Based Views): 클래스 기반 뷰
- 장점
  - 코드 확장과 재사용 용
  - 다중 상속, Mixin 가
  - 내장 Classe Based View 사용(ListView, CreateView, DetailView...)
- 단점
  - 읽기 어려우며 복잡도가 높
  - 데코레이터 사용 시 함수를 재정의 해야함
 
>일반적인 생성, 조회, 수정, 삭제 등의 View에 적합

## Template는 서버에서 실행함
- Template 태그
  - block : 자식 템플릿으로 재정의할 수 있는 블록 > {%block name%}{%endblock%}
  - extends : 부모 템플릿을 확장, 상속 >
  - include : 템플릿을 로드하고 현재 Context로 렌더링, 템플릿 포함 >
  - for : Context 변수의 배열의 항목을 반복 사용 *for, empty >
  - if : 조건이 true이면 출력하고 false인 경우 미출력 *if, else, elif >
  - url : 보기 및 선택적 매개변수와 일치하는 절대 경로 참조(도메인 이름이 없는 URL)를 반환
    
- Template 태그
  - 부모 HTML을 자식 HTML이 상속받음
    
- Template 필터
  - date : 주어진 형식에 따라 날짜 형식을 지정 >>> {{value|date:"D d M Y"}}
  - default : 값이 없을 때, 지정된 기본값을 사용, 값이 있을 경우, 값을 출력함 >>> {{value|default:"nothing"}}
  - center : 주어진 너비의 필드에서 값을 가운데에 맞춤 >>> {{value|center:"15"}}
  - truncatechars : 지정된 문자 수보다 긴 경우 문자열을 자름. 자른 문자열은 번역 가능한 줄임표 문자("...")로 끝남 >>> {{value|truncatechars:7}}
  - intcomma : 정수 또는 부동 소수점(또는 둘 중 하나의 문자열 표현)을 세 자리마다 쉼표가 포함된 문자열로 변환 >>> {%load humanize%} or {{{{value|intcomma}}

  
# TECHIT 7주차 강의 기록 <br>Chapter 5. 백엔드의 필수: CRUD 개발하기

