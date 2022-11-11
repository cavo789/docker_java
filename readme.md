# Play with Docker and Java

**Personal learning**

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



