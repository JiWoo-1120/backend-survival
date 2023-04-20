# [@RequestMapping](https://www.iana.org/assignments/media-types/media-types.xhtml)
특정 url로부터 요청을 받으면 어떤 Controller에서 처리할 지 알아야 한다.
이 때, 특정 url을 요청을 수행할 Controller과 매핑하여 지정하는 어노테이션이 @RequestMapping이다.
    @GetMapping
    HTTP GET 요청을 특정 핸들러 메서드에 매핑하기 위한 어노테이션
    @PostMapping
    @PatchMapping
    @DeleteMapping
    @PathVariable
    - URL 경로에 변수를 넣어주는 것이다.
    - @PathVariable 어노테이션을 이용해서 {템플릿 변수} 와 동일한 이름을 갖는 파라미터를 추가하면 된다.
    </br><img src="/IMG/차이점.png" ></img>

# @RequestBody와 @ResponseBody 차이점

클라이언트 -> 서버 요청 : @RequestBody
* 어노테이션은 HTTP 요청의 body를 자바 객체로 변환해주는 역할을 합니다. 즉, HTTP 요청의 body에 담긴 데이터를 자바 객체로 매핑하여 컨트롤러 메서드의 파라미터로 전달할 수 있도록 합니다.

서버 -> 클라이언트 응답 : @ResponseBody
* 어노테이션은 컨트롤러 메서드에서 반환하는 데이터를 HTTP 응답의 body에 넣어주는 역할을 합니다. 즉, 컨트롤러 메서드에서 반환하는 데이터를 HTTP 응답의 body에 담아 클라이언트에게 전송할 수 있도록 합니다.

# @ExceptionHandler
Spring Framework에서 예외 처리를 담당하는 어노테이션

# @ResponseStatus
* Spring Framework에서 HTTP 응답의 상태 코드를 지정하는 어노테이션
*  컨트롤러에서 반환하는 결과에 대한 HTTP 응답 상태 코드를 지정할 수 있다.
ex. @ResponseStatus(HttpStatus.OK)와 같이 메서드나 클래스에 적용하여 HTTP 응답의 상태 코드를 200 OK로 지정할 수 있다.