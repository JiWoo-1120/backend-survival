# 1. Listen
다른 곳에 접속하는 것이 아니라 포트 번호만 정하면된다.

### Java ServerSocket
    Java에서는 ServerSocket이라는 별도의 클래스를 사용한다.
    (Socket을 상속한게 아니라, 완전히 구별된다는 점에 주의)
    자바에서는 소켓을 열긴여는데 서버소켓이란느 별도의 소켓을 사용한다.
    그냥 리슨만 하기위해 따로 준비해둔것이다.

### Blocking
I/O에서 아래의 이미지와 같이 socket이 다음명령을 잡고있다.
이렇게 다음 응답을 기다리는 걸 Blocking이라고 한다.
        
>    ### socket 다음에 나와야할 "Accept!"이 나오지 않는다.
>    <img src="/IMG/blocking_ex1.png" width="450px" height="300px"></img>
>    <img src="/IMG/blocking_ex1_1.png" width="450px" height="300px"></img><br/>
        
>    ### socket 전에 "Accept!"을 입력해서 출력되었다.
>    <img src="/IMG/blocking_ex1.png" width="450px" height="300px"></img>
>    <img src="/IMG/blocking_ex1_1.png" width="450px" height="300px"></img><br/>
```java
     ServerSocket listener = new ServerSocket(8080, 0);
```

# 2. Request
서버는 요청을 하는게 아니라, 요청을 받는 입장!
받으면 읽어야지. 따라서 먼저 읽는다.
```java
Reader reader = new InputStreamReader(socket.getInputStream());

            CharBuffer charBuffer = CharBuffer.allocate(1_000_000);
            reader.read(charBuffer);

            charBuffer.flip();
            System.out.println(charBuffer.toString());
```
# 3. Response
응답 메세지를 만들어서 전송한다.
```java
String body = "Hello, world!";
byte[] bytes = body.getBytes();
String message = "" +
	"HTTP/1.1 200 OK\n" +
	"Content-Type: text/html; charset=UTF-8\n" +
	"Content-Length: " + bytes.length + "\n" +
	"\n" +
	body;
```
⚠️ Content-Length로 정확한 크기를 알 수 있기 때문에 마지막 줄에 Newline(\n)을 넣지 않아도 된다.

# 4. Close
```java
socket.close();
```