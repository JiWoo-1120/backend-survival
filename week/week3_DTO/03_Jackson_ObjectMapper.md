# Jackson ObjectMapper 란
 Dto → JSON(문자열) 변환
 JSON(문자열) → Dto 변환

 * 필드보다는 getter 메서드의 이름을 따른다
 * JSON의 스키마를 작성한다는 느낌으로 만들면 된다.

### JSON 스키마
```JAVA
{
	"id": "1234",
	"title": "제목",
	"content": "테스트"
}
```
### Java 코드
```JAVA
	public class PostDto {
	private String id;

	private String title;

	private String content;

	public PostDto() {
	}

	public PostDto(String id, String title, String content) {
		this.id = id;
		this.title = title;
		this.content = content;
	}
	
	public String getId() {
		return id;
	}

	public String getTitle() {
		return title;
	}

	public String getContent() {
		return content;
	}
}
```

Spring DI(Dependency Injection)를 통해 컨트롤러에서 Jackson ObjectMapper를 얻는다. 스프링이 등록된 객체(Bean)를 관리하고 있고, 생성자에 명시하면 받아서 사용할 수 있다.
사용=의존성/의존관계를 주입 받는다
```JAVA
public class PostController {
	private final ObjectMapper objectMapper;
	
	public PostController(ObjectMapper objectMapper) {
		this.objectMapper = objectMapper;
	}
```

우리가 Jackson을 바로 쓸 수 있는 건 Spring Boot가 Jackson을 지원하기 때문. 변환 또한 Spring Boot가 알아서 해주기 때문에 실제로는 아주 쉽고 자연스럽게 쓸 수 있다.
### `GetMapping`
_objectMapper.writeValueAsString(postDto);_ : Dto를 String으로 바꿔준다.
```JAVA
    @GetMapping("/{id}")
	public String detail(@PathVariable String id) throws JacksonException {
    PostDto postDto = new PostDto(id, "제목", "내용");
		
    return objectMapper.writeValueAsString(postDto);
	}
```
Jackson ObjectMapper는 web 의존성에 이미 선언되어잇다.
그렇기 때문에 위의 코드처럼 objectMapper.writeValueAsString(postDto); 사용해주지 않아도 된다.

아래의 코드처럼 Dto만 선언해줘도 Spring Boot가 알아서 변환해준다.
```JAVA
	@GetMapping("/{id}")
	public PostDto detail(@PathVariable String id) throws JacksonException {
    PostDto postDto = new PostDto(id, "제목", "내용");

    return postDto;
	}
```

### `PostMapping`
_objectMapper.readValue(body, PostDto.class);_ : body에서 넘어온 값 읽기
body에 있는 데이터 타입을 알아야하기 때문에 Dto를 명시해준다.
```JAVA
	@PostMapping
	@ResponseStatus(HttpStatus.CREATED)
	public PostDto create(@RequestBody String body) throws JacksonException {
		PostDto postDto = objectMapper.readValue(body, PostDto.class);
		
		return postDto;
	}
```
`@GetMapping`에서 설명했던 개념과 동일하게
Spring Boot가 알아서 변환해준다.
```JAVA
   	@PostMapping
	@ResponseStatus(HttpStatus.CREATED)
	public PostDto create(@RequestBody PostDto postDto) {
		return postDto;
	}
```

# `@JsonProperty`
프런트에서 넘어오는 JSON형식의 데이터명과 DTO에 선언되어있는 명이 다를 경우 사용해준다.
```JAVA
    @JsonProperty("post_content")
    public String getContent() {
        return content;
    }
```
이러헥 해준면 "post_content"는 Dto에서는 content로 사용 가능하다.