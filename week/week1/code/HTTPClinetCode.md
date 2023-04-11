
public class App {
    public static void main(String[] args) throws IOException {

        App app = new App();
        app.run();
    }

    private void run() throws IOException {

        System.out.println("Hello World!");

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
    }
}
