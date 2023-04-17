# API(Application Programming Interface)
어플리케이션을 만들기 위한 인터페이스

### Interface를 사용하면 얻을 수 있는 효과
- Communication
    필요한 것을 소통하기 위한 것
- Specification
    연결점만 있는 것
- Information Hiding (Principle)
    정보은닉은 어딘가의 뒤로 숨기는 걸 의미
    벽 뒤에 숨어있다 느낌(내부라는 것이 존재하지 않는다.)
- Encapsulation (Technique)
    기술적으로 정보은닉을 하는 방법 중에 하나가 캡슐화라고 한다.
    캡슐화는 하나로 묶어서 내부와 외부를 이어주는 인터페이스를 통해서만 정보를 처리하는 것을 캡슐화
- Implementation
    임플리멘테이션과 구분하기위해 인터페이스를 사용한다.

# REST(Representational State Transfer)
네트워크베이스 소프트웨어 아키텍처에서 필요한 아키텍처 스타일
## Architecture와 Architecture Style의 차이
Architecture와 Architecture Style은 다르다!
설계를 할 때(Architecture) 공통된 방법을 사용한 것, 그 공통된 방법이 Architecture Style이다.
### 제약조건
## 1장 : Software Architecture
아키텍처 스타일(architectural style)이란, 그 스타일을 따르는 아키텍처가 지켜야 하는 제약조건들의 집합이다.
## 2장 : Network-based Application Architectures
* 아키텍처 스타일의 적용 범위는 네트워크 기반 애플리케이션(Network-based Application)으로 한정된다.
* 네트워크 기반 소프트웨어는 operation이 네트워크를 경유해서 일어난다는 사실을 사용자에게 감출 필요가 없다. 분산(distributed) 소프트웨어는 감추어야한다.
* 애플리케이션이기 때문에, OS나 네트워킹 소프트웨어 같은 것은 고려 대상에서 제외된다.
* 네트워크 기반 애플리케이션 아키텍처의 관심 사항은 다음과 같다.
    - 성능
    - 규모확장성(Scalability)
    - 단순성
    - 수정용이성(Modifiability)
    - 가시성(Visibility)
    - 이식성(Portability)
    - 신뢰성(Reliability)
## 3장 :Network-based Architectural Styles
이 장에서는 Pipe and Filter, Layered-Client-Cache-Stateless-Server, Code on Demand 를 비롯한 여러가지 네트워크 기반 아키텍처 스타일들을 소개한다.
## 4장 :Designing the Web Architecture: Problems and Insights
이 장에서는 웹 아키텍처의 요구사항, 해결해야할 문제를 설명하고 이를 해결하기 위한 접근 방법을 제시한다.
## 5장 : Representational State Transfer (REST)
4장에서 제시한 접근방법의 결과물로 웹을 위한 아키텍처 스타일 “REST”를 소개한다. REST는 3장에서 소개했던 네트워크 기반 아키텍처 스타일들 몇 가지와 추가로 Uniform Interface 스타일을 함께 결합한 하이브리드 스타일이다.
### Client-Server
클라이언트-서버 스타일은 사용자 인터페이스에 대한 관심(concern)을 데이터 저장에 대한 관심으로부터 분리함으로써 클라이언트의 이식성과 서버의 규모확장성을 개선한다.
### Stateless 
* 클라이언트와 서버의 통신에는 상태가 없어야한다.
* 모든 요청은 필요한 모든 정보를 담고 있어야한다.
* 가시성 개선 - 요청 하나만 봐도 바로 뭔지 알 수 있다.
* 신뢰성 개선 - task 실패시 복원이 쉽다.
* 규모확장성 개선 - 상태를 저장할 필요가 없다.
### Cache
* 캐시가 가능해야한다.
즉 모든 서버 응답은 캐시 가능한지 그렇지 아닌지 알 수 있어야한다.
* 호율, 규모확장성, 사용자 입장에서의 성능이 개선된다.
### Uniform Interface
* 구성요소(클라이언트, 서버 등) 사이의 인터페이스는 균일(uniform)해야한다.
* 인터페이스를 일반화함으로써 얻을 수 있는 것
    - 상호작용의 가시성이 개선
    - 구현과 서비스가 분리되므로 독립적인 진화가 가능
### Layered System
* 계층(hierarchical layers)으로 구성이 가능해야하며,
각 레이어에 속한 구성요소는 인접하지 않은 레이어의 구성요소를 볼 수 없어야한다.
### Code-On-Demand (Optional)
* 계층(hierarchical layers)으로 구성이 가능해야하며,
서버가 네트워크를 통해 클라이언트에 프로그램을 전달하면 그 프로그램이 클라이언트에서 실행될 수 있어야한다.

## 6장: Experience and Evaluation
REST 아키텍처 스타일은 URI, HTTP 등의 웹 표준에 반영되었다.

# 필딩 제약 조건
4가지 인터페이스 제약이있다.
1. Identification of Resources → URI 등으로 리소스를 식별할 수 있다.
2. Manipulation of Resources through Representations → 표현으로 리소스를 조작한다.
3. Self-descriptive Messages
메시지는 자기서술적이기 때문에 여러 레이어에서 처리/변환 가능하다.
4. Hypermedia as the Engine of Application State → 줄여서 HATEOAS라고 부른다. REST API를 이야기할 때 까다로운 부분 중 하나.