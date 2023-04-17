# URI (Uniform Resource Identifier)
리소스를 식별하는 방법
식별할 때는 식별자(Identifier = ID)를 활용한다.

URL은 크게 둘로 나뉜다.
1. URL(Uniform Rewource Locator) → 리소스의 위치. 위치 변경에 취약함
    https://developer.mozilla.org
    https://developer.mozilla.org/en-US/docs/Learn/
    https://developer.mozilla.org/en-US/search?q=URL
2. URN(Uniform Resource Name) → 리스소의 "유니크"한 이름. 사실상 잘 쓰이지 않음.
    urn:isbn:9780141036144
    urn:ietf:rfc:7230
    ex. 음반, 책 등

# MIME (Content Type, Media Type)
* 리소스를 표현
* 서버에 요청할때도 동일하게 넣어준다.
* MIME 타입은 문서 타입 정보를 실어나르는 유일한 방법은 아닙니다.

[IANA](https://www.iana.org/assignments/media-types/media-types.xhtml, "IANA")에 등록된 것들을 참고하자
1. `text/plain` ⇒ E-mail에서 자주 사용.
2. `text/html` ⇒ 일반적인 웹 문서. HTML 문서.
3. `text/css`
4. `text/javascript`
5. `application/xml` ⇒ 범용. 자기서술적이기 상대적으로 어렵다.
6. `application/atom+xml`
7. `application/json` ⇒ 범용. 자기서술적이기 굉장히 어렵다.
8. `application/dns+json`