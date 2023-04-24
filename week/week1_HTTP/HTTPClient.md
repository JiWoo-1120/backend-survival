# TCP/IP 통신
    인터넷 프로토콜 스위트(Internet Protocol Suite)
<img src="/IMG/internet_protocol_suite.png" width="60%" height="55%" title="인터넷 프로토콜 스위트" alt="인터넷 프로토콜 스위트"></img><br/>
이중에서 제일 유명한 TCP와 IP를 이용해서 인터넷 프로토콜 스위트를 부른다.

---------------------------------------

## TCP(스트림)와 UDP(데이터그램)
- 전송 계층의 프로토콜
- __연결여부에 차이점이 있다__

>    * ### TCP
>    - 양방향으로 바이트 스트림을 전송
>    - 연결이 필요하다. 전달 및 순서 보장.
>    - 전화 = 전화를 걸었을 때 상대방이 전화를 받아야함. 전화를 받으면 받았는지 확인을 바로 할 수 있음
>    * ### UDP
>    - 비연결형소켓
>    - 연결하지 않고 데이터를 보냄. 전달 및 순서를 보장하지 않는다.
>    - 편지 = 편지를 여러장 보내면 뭐가 먼저 도착하는지 알 수 없음. 상대방이 확인했는지 알 수 없음

---------------------------------------

## Socket과 Socket API
네트워크로 통신을 할때 여러 계층을 통해서 한다.
    
>    ###### Socket이란?
>    네트워크 세계로 데이터를 내보내거나 받기 위한 실제적인 창구이다.
>    그러므로 프로세스가 데이터를 보내거나 받기 위해서는
>    소켓을 열고 소켓에 데이터를 보내고 소켓으로부터 데이터를 읽어들여야한다.
>    소켓은 프로토콜, IP 주소, 포트 넘버로 정의된다.

>   ###### 프로토콜
>   어떤 시스템이 다른 시스템과 통신을 원활하게 수용하도록 해주는 통신 규약, 약속
>   ###### IP
>   전 세계 컴퓨터에 부여된 고유의 식별 주소
>   ###### 포트
>   - 같은 컴퓨터 내에서 프로그램을 식별하는 번호
>   - 내부적으로 프로세스가 할당받아야 하는 고유한 숫자 

>### Socket
>####    : 기본적으로 파일과 유사하게 다룰 수 있다.(유닉스에서는 파일 디스크립터의 일종)
>   종착점
>   읽고, 쓰고, 닫고 파일을 다루는 것과 유사하다.

>### Socket API
>####   : Socket을 다루기 위한 API
>    Berkeley sockets


>####    TCP 통신 순서
>    1. Listen 
>       서버는 접속 요청을 받기 위한 소켓을 연다.
>    2. Connect
>        클라이언트는 소켓을 만들고, 서버에 접속을 요청한다.
>    3. Accept
>        서버는 접속 요청을 받아서 클라이언트와 통신할 소켓을 따로 만든다.
>    4. __Send & Receive 반복__
>        소켓을 통해 서로 데이터를 주고 받는다.
>    5. Close
>        통신을 마치면 소켓을 닫는다.
>        상대방은 Receive로 인지할 수 있다.

---------------------------------------

## URI와 URL

### 클라이언트(고객) → 요청
### 서버(서비스를 전달하는 사람) → (처리) → 응답

여기서 처리하는 것은?
    __보내온 요청인 서비스/리소스를 처리한는 것 -> URL__
        리소스 : 서비스의 자세한 내용
        URL : 리소스를 보내기 위해서 가장 많이 사용하는 방법

---------------------------------------

## 호스트(host)
도메인이라고 부른 것이 호스트

# 1. Connect
소켓을 열어준다.
Socket socket = new Socket("example.com", 80);

# 2. Request
요청메세지 만들어서 보내기
url 에 담아서 보낸다.

#### path(경로)
http://example.com/

url 마지막에 /를 꼭써줘야한다.
(http://example.com 만 써도 브라우저 알아서 뒤에 /를 붙혀줌)

#### 최신자바
```java
  String msg = """
                GET / HTTP/1.1
                Host: example.com
                빈줄 꼭 넣어줘야함
                """;
```

#### 기존
```java
 String msg = "" +
                "GET / HTTP/1.1\n" +
                "Host: example.com\n" +
                "\n";
```

소켓에서 Output Stream을 얻어서 쓸 수 있다.
```java
OutputStream outputStream = socket.getOutputStream();
outputStream.write(msg.getBytes());
```


문자열을 직접 전송하고 싶다면 Writer쓴다.
```java
OutputStream outputStream = socket.getOutputStream();
Writer writer = new OutputStreamWriter(outputStream);
```

*내부적으로 버퍼가 있기 때문에 flush 를 잊지 않아야 한다.*

# 3. Response
소켓에서 Input Stream을 얻어서 쓸 수 있다.

```java
InputStream inputStream = socket.getInputStream();

byte[] bytes = new byte[1_000_000];
int size = inputStream.read(bytes);

byte[] data = Arrays.copyOf(bytes, size);
String txt = new String(data);
```

모든 설정을 마친 후 돌려보면 아래 이미지와 같은 결과가 나오고
빈줄을 꼭 넣어줘야 한다는 강조가 왜 인지 알 수 있다.
<img src="/IMG/빈줄.png" width="60%" height="55%" title="빈줄" alt="빈줄"></img><br/>



요청과 마찬가지로 Reader를 쓰면 훨씬 편하다.
중요 : CharBuffer를 toString()하기 전에 flip()을 해준다!

```java
InputStream inputStream = socket.getInputStream();
Reader reader = new InputStreamReader(inputStream);

CharBuffer charBuffer = CharBuffer.allocate(1_000_000);

reader.read(charBuffer);

charBuffer.flip();

String txt = charBuffer.toString();

System.out.println(txt);
```

# 4. Close
 ### Java try-with-resources
try 구문에섬나 socket를 쓰고 나가는 순간 close를 시켜준다.
```java
try (Socket socket = new Socket(host, port)) {
     // Request
     // Response
}
```
```java
try (Socket socket = new Socket("example.com", 80)) {

           System.out.println("Connect!");

           String msg = "" +
                   "GET / HTTP/1.1\n" +
                   "Host: example.com\n" +
                   "\n";

           OutputStream outputStream = socket.getOutputStream();
           Writer writer = new OutputStreamWriter(outputStream);

           writer.write(msg);
           writer.flush();


           System.out.println("Request!");

           InputStream inputStream = socket.getInputStream();
           Reader reader = new InputStreamReader(inputStream);

           CharBuffer charBuffer = CharBuffer.allocate(1_000_000);

           reader.read(charBuffer);

           charBuffer.flip();

           String txt = charBuffer.toString();

           System.out.println(txt);


       }
        System.out.println("Complete!");
```