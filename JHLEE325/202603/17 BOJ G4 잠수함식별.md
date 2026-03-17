```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String sound = br.readLine();

        String regex = "(100+1+|01)+";

        if (sound.matches(regex)) {
            System.out.println("SUBMARINE");
        } else {
            System.out.println("NOISE");
        }
    }
}
```
