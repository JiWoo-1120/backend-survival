```java
@RestController
@RequestMapping("/posts")
public class PostController {

    @GetMapping
    public String list() {
        return "게시물 목록";
    } 

    @GetMapping("/{id}")
    public String detail(@PathVariable("id") String id) {
        return "게시물 상세: " + id;
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public String create(@RequestBody String body) {
        return "{\"action\": \"게시물생성\", \"body\": \"" +
                body.replace("\"", "\\\"") + "\"}";
    }

    @PatchMapping("/{id}")
    public String update(@PathVariable("id") String id, @RequestBody String body) {
        return "{\"action\": \"게시물 수정 " + id + "\", \"body\": \"" +
                body.replace("\"", "\\\"") + "\"}";
    }

    @DeleteMapping("/{id}")
    public String delete(@PathVariable("id") String id) {
        return "게시물 삭제: " + id;
    }

}
```
