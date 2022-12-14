# Play with Docker and Java

![Banner](./banner.svg)

## How to

1. Create a new folder on your machine
2. Create a file called `Main.java` with this content

```java
public class Main
{
     public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

3. On the command line, run `docker run --rm -v $PWD:/app -w /app openjdk:11 javac Main.java` to download (the first time the `openjdk` Docker image). The command will then run the `javac` command and will compile your `Main.java` source into `Main.class`
4. Run `docker run --rm -v $PWD:/app -w /app openjdk:11 java Main` to run it.

## Call REST API

1. Create a new file called `API.java` with this content

```java
package restclient;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class API {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://jsonplaceholder.typicode.com/todos/1");//your url i.e fetch data from .
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setRequestProperty("Accept", "application/json");
            if (conn.getResponseCode() != 200) {
                throw new RuntimeException("Failed : HTTP Error code : "
                        + conn.getResponseCode());
            }
            InputStreamReader in = new InputStreamReader(conn.getInputStream());
            BufferedReader br = new BufferedReader(in);
            String output;
            while ((output = br.readLine()) != null) {
                System.out.println(output);
            }
            conn.disconnect();

        } catch (Exception e) {
            System.out.println("Exception in NetClientGet:- " + e);
        }
    }
}

```

2. On the command line, run `docker run --rm -v $PWD:/app -w /app openjdk:11 javac API.java` to compile your `API.java` source into `API.class`
3. Run `docker run --rm -v $PWD:/app -w /app openjdk:11 java API.java` to run it.

This example will use the sample `https://jsonplaceholder.typicode.com/todos/1` to generate one fake TODO. The JSON will be displayed on the command line.

![TODO](./images/todo-json.png)
