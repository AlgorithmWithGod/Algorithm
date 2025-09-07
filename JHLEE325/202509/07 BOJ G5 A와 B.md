```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        String s = br.readLine();
        String t = br.readLine();

        StringBuilder sb = new StringBuilder();
        sb.append(t);

        while (s.length() < sb.length()) {
            char lastChar = sb.charAt(sb.length() - 1);

            sb.deleteCharAt(sb.length() - 1);

            if (lastChar == 'B') {
                sb.reverse();
            }
        }

        if (s.equals(sb.toString())) {
            System.out.println(1);
        } else {
            System.out.println(0);
        }
    }
}

```
