# Java HTTP Server
- JDK-specitic HTTP server API
- 고수준의 API
- 내부적으로 NIO를 사용하는 고수준 HTTP 서버 API

## Java - NIO Non-blocking I/O


---------------------------------------

# 1. 서버 객체 준비
```java
    InetSocketAddress address = new InetSocketAddress(8080);
    HttpServer httpServer = HttpServer.create(address, 0);
    // 예시
    // int backlog = 0;
    // HttpServer httpServer = HttpServer.create(address, backlog);
```

# 2. URL(정확히는 path)에 핸들러 지정
path('/')에 대한 핸들러를 말하는거다.

## Request
```java
//1. Request
    String method = exchange.getRequestMethod();
    System.out.println("Method: " + method);

    URI uri = exchange.getRequestURI();
    String path = uri.getPath();
    System.out.println("Path: " + path);

    Headers headers = exchange.getResponseHeaders();
    for (String key : headers.keySet()) {
        List<String> val = headers.get(key);
        System.out.println(key + " : " + val);
    }

    InputStream inputStream = exchange.getRequestBody();

    byte[] bytes = inputStream.readAllBytes();
    String body = new String(bytes);

    System.out.println(body);
```

## Response
Satus Code와 Content-Length 지정해줘야한다.
```java
// 2. Response
    String content = "hahahaha\n";
    byte[] bytes1 = content.getBytes();

    exchange.sendResponseHeaders(200, bytes1.length);

    OutputStream outputstream = exchange.getResponseBody();
    outputstream.write(bytes1);
    outputstream.flush();
```