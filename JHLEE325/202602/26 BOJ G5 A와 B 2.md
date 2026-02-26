```java
import java.io.*;
import java.util.*;

public class Main {
    static String S, T;
    static int answer = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        S = br.readLine();
        T = br.readLine();

        solve(T);
        System.out.println(answer);
    }

    static void solve(String cur) {
        if (cur.length() == S.length()) {
            if (cur.equals(S)) {
                answer = 1;
            }
            return;
        }

        if (answer == 1) return;

        if (cur.charAt(cur.length() - 1) == 'A') {
            solve(cur.substring(0, cur.length() - 1));
        }

        if (cur.charAt(0) == 'B') {
            String next = cur.substring(1);
            StringBuilder sb = new StringBuilder(next);
            solve(sb.reverse().toString());
        }
    }
}
```
