```java
public class App {
    public static void main(String[] args) throws IOException {
        App app = new App();
        app.run();
    }

    private void run() throws IOException {
        // 1. Listen
        ServerSocket listener = new ServerSocket(8080, 0);
        System.out.println("Listen!");

        // 2. Accept
        Socket socket = listener.accept();
        System.out.println("Accept!");

        while (true) {

            // 3. Request
            Reader reader = new InputStreamReader(socket.getInputStream());

            CharBuffer charBuffer = CharBuffer.allocate(1_000_000);
            reader.read(charBuffer);

            charBuffer.flip();
            System.out.println(charBuffer.toString());

            // 4. Response
            String body = "Hello, world!";
            byte[] bytes = body.getBytes();
            String msg = "" +
                    "HTTP/1.1 200 OK\n" +
                    "Content-Type: text/html; charset=UTF-8\n" +
                    "Content-Length: " + bytes.length + "\n" +
                    "\n" +
                    body;

            Writer writer = new OutputStreamWriter(socket.getOutputStream());
            writer.write(msg);
            writer.flush();

            // 5. Close
            socket.close();
        }
    }
}
```
