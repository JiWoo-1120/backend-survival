# CORS(Cross-Origin Resource Sharing)
_Same-Origin Policy(동일출처 정책)_ 에 위배되었을 때 에러가난다.
이때, CORS를 사용하면 서로 다른 Origin에서 리소스를 쉐어해 해결해준다.

## _Same-Origin Policy(동일출처 정책)_란?
어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 _웹 브라우저에서 제한하는 중요한 보안 방식_
여기서 출처란?
두 URL의 프로토콜, 포트 (en-US)(명시한 경우), 호스트 (en-US)가 모두 같아야 동일한 출처

1. 서버에 API 요청을 한다.
2. 서버는 응답을 해주긴한다.
3. 웹 브라우저에서 Same-Origin Policy에 위배되는지 확인한다.

아래의 이미지는 출처가 달라 Same-Origin Policy에 위배된다.
그래서 웹 브라우저가 에러를 보낸다.
<img src="/IMG/Same_Origin_Policy.png"></img>

쉽게말하자면 내가 띄운 서버에서 보낸 요청 주소와 현재 내가 들어와있는 페이지 주소가 같아야한다.

### 해결 방법인 CORS를 사용하자.
B/E에서 RestAPI의 응답 헤더 “Access-Control-Allow-Origin” 속성을 포함시키자!
<img src="/IMG/DDD.png"></img>
- 웹 페이지 (F/E): https://ahastudio.com
- API 서버 (B/E): https://api.ahastudio.com
응답 메세지
```JAVA
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://ahastudio.com
(...자세한 헤더는 생략…)
(빈 줄)
[
	{
		"id": "123",
		"title": "재밌는 이야기",
		"content": "는 다음 기회에…"
	}
]
```
    “Access-Control-Allow-Origin”는 '아~ F/E(Origin) 쟤네는 RestAPI 사용해도 괜찮습니다~' 라고 알려주는 방식이다.


# Spring Web MVC에서 CORS

## HttpServletResponse
```JAVA
@GetMapping
public List<PostDto> list(HttpServletResponse response) {
	response.addHeader("Access-Control-Allow-Origin", "http://localhost:3000");
}
```
Origin과 무관하게 모든 요청을 허용할 거면 그냥 “*”로 잡아주면 된다.
```java
response.addHeader("Access-Control-Allow-Origin", "*");
```

## @CrossOrigin
Spring Web에선 @CrossOrigin 애너테이션을 써주면 된다. 클래스, 메서드 모두 지정 가능.
```java
@CrossOrigin("http://localhost:3000")
```
모든 요청을 허용할 거라면 마찬가지로 “*”로 잡아주거나 안써도됨.
```java
@CrossOrigin("*")
@CrossOrigin
```

## WebMvcConfigurer
WebMvcConfigurer 인터페이스에 대한 Spring Bean으로 환경 설정.
```java
@Bean
	public WebMvcConfigurer webMvcConfigurer() {
		return new WebMvcConfigurer() {
		
		@Override
		public void addCorsMappings(CorsRegistry registry) {
			registry.addMapping("/**")
							.allowedMethods("GET", "POST", "PATCH", "DELETE", "OPTIONS")
							.allowedOrigins("http://localhost:3000");
		}
	};
}
```