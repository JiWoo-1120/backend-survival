# Spring
*JAVA로 다양한 어플리케이션을 만들기 위한 프로그래밍 틀이라 할 수 있다.*
Spring 프레임워크 프로젝트 자체를 지칭하는데 사용될 수 있다.
"Spring"이라고 할 때 프로젝트 제품군 전체를 의미한다.
- 작업방식에 대한 유연성
- 버전 간에 큰 변화가 거의 없음(유지 보수를 용이하게 함)

# Spring Boot
- Spring Boot의 도움으로 서블릿 컨테이너가 내장
- 프로덕션에 바로 사용할 수 있는 Spring 기반 애플리케이션을 빠르게(그리고 자유롭게) 만들 수 있는 방법을 제공한다.
- Spring 프레임워크를 기반으로 하며, 구성보다 규칙을 선호하며, 가능한 한 빨리 시작하고 실행할 수 있도록 설계되어있다.

# Spring initializr
스프링 프로젝트를 쉽게 생성할 수 있게 도와준다.
</br><img src="/IMG/Spring initializr.png" ></img>

# Web Server와 WAS(Web Application Server)
## Web Server
소프트웨어와 하드웨어로 구분된다.
- 하드웨어
Web 서버가 설치되어 있는 컴퓨터
- 소프트웨어
웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램
- HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당한다.
    
## WAS(Web Application Server)
- WAS = Web Server + Web Container
- DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
- HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다.
- “웹 컨테이너(Web Container)” 혹은 “서블릿 컨테이너(Servlet Container)”라고도 불린다.
    
    ##  Tomcat
    톰캣은 아파치 소프트웨어 재단의 웹 어플리케이션 서버(와스)로서, 
    자바 서블릿을 실행키고 JSP코드가 포함되어 있는 웹 페이지를 만들어준다. 

[Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html, "study")
---------------------------------------
# Spring MVC
## Model-View-Controller 아키텍처 패턴
    1. view 화면
    2. Controller 입력
    3. Model 그 외의 모든것
        모델에 핵심 비즈니스가 들어간다.
    # 관심사의 분리(Seperation of Concern)
---------------------------------------
# Java Annotation
어노테이션을 직접 타고 들어가면 어떤 것들이 포함되어있는지 파악할 수 있다.
##   @RestController
###    @Controller
###    @ResponseBody
Body에 있는 것을 직접적으로 response(응답)해줄거야~!
</br><img src="/IMG/RestController.png" ></img>

# @GetMapping
##   @RequestMapping

<img src="/IMG/겟매핑,리퀘스트매핑.png" ></img>

