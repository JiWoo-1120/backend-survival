# DTO (Data Transfer Object)
> 제약조건
> “between processes”
> “working with a remote interface, such as Remote Facade”
> 다른 프로세스와 통신, 그것도 원격(네트워크를 통해)으로!

여기서 프로세스 간의 통신은 IPC (Inter-Process Communication)라 부른다.
## IPC (Inter-Process Communication)
* B/E와 F/E로 Tier를 나누면 IPC가 필수적이다.
* 프로세스간의 통신
* File → 가장 기본적인 접근. 원격 환경에서 활용하기 어렵다.
* Socket → 파일과 유사하게 읽고 쓸 수 있지만, 원격 환경에서도 활용할 수 있다.
    * HTTP 같은 고수준 프로토콜을 활용하면 어느 정도 정해진 틀이 있기 때문에 상대적으로 쉬워진다.
    * REST를 활용하면 RPC(SOAP의 일반적인 활용)가 아닌 Resource에 대한 CRUD로 정리해야 함.

    우리는 원격 환경에서 프로세스가 통신하는 걸 할거다!

REST에선 표현을 다뤄야 하고, 이를 위해 데이터를 담는 것 외엔 사실상 아무 것도 하지 않아서 제대로 된 객체라고 볼 수 없는 (하지만 Java에선 어쩔 수 없이 class를 활용해서 쓸 수 밖에 없는) 특별한 객체를 사용하게 된다.

그저 데이터의 덩어리가 될 수 있다. 이런 경우를
## 무기력한 도메인 모델
도메인 모델 패턴을 사용할 때 발생할 수 있는 안티 패턴 중 하나
1. 도메인 모델의 복잡성을 제거하다 보니, 서비스 계층이 과도하게 복잡해지는 문제가 발생할 수 있다.
2. 도메인 모델 객체가 단순화되어, 객체 지향 프로그래밍의 장점을 활용할 수 없게 된다.
3. 비즈니스 로직이 서비스 계층에서 처리되면, 도메인 모델 객체의 역할이 제한된다.
4. 유지보수성이 떨어지며, 코드의 가독성이 떨어진다.

# DTO
* 아주 단순하게 보면 setter와 getter로만 이뤄짐.
* JavaBeans에서 유래한 Java Bean 또는 그냥 Bean이라고 부르는 형태에 가까움(Spring Bean, POJO와 다름에 주의!)
* 제대로 된 객체가 아니라 그냥 무기력한 데이터 덩어리. 

    _자바빈즈(JavaBeans)_ 와 _EJB(Enterprise JavaBeans)_ 는 모두 자바에서 재사용 가능한 컴포넌트를 만들기 위한 방법론
* *자바빈즈(JavaBeans)*
    * 주로 프론트엔드에서 사용되는 컴포넌트로, UI와 데이터를 연결하는 역할을 합니다.
    * 프론트엔드와 백엔드 간의 데이터 전송을 담당
* *EJB(Enterprise JavaBeans)*
    * 백엔드에서 사용되는 서버 사이드 컴포넌트로, 엔터프라이즈 애플리케이션의 백엔드 역할을 담당
    * 백엔드에서 필요한 업무 로직을 구현하는 데에 사용

## Tier간 통신
* F/E와 B/E 사이
    * DTO 자체를 그대로 전송할 수는 없고, 직렬화(마샬링)를 통해야 한다.
    * 떤 직렬화 기술을 사용할 건지도 결정해야 함. → XML, JSON
* B/E와 DB 사이
    * 옛날에는 DTO를 VO라 부르기도했다.
    * JPA를 지양하고 DDD를 따르는 사람 중 일부는 ORM(JPA, 하이버네이트)은 Active Record + DTO처럼 접근.

    ### DDD(Domain-driven Design)
    * 도메인 모델을 중심으로 소프트웨어를 설계
    * 도메인 모델과 다른 레이어를 분리하여 구현
    * 다른 레이어와 분리하여 유연성과 확장성을 높이는 것을 강조합니다.

    ### ORM(Object-Relational Mapping)
    * 데이터베이스와 객체 간의 매핑을 수행
    * 데이터베이스와 객체 지향 프로그래밍 간의 변환을 수행
    * JPA와 Hibernate는 대표적인 ORM 프레임워크
    * 개발 생산성이 높아지고 유지보수가 쉬워지지만, 데이터베이스와 객체 지향 프로그래밍 간의 차이로 인해 발생하는 문제들이 존재