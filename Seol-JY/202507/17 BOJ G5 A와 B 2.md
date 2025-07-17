```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    static int K;
    static String S, T;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        S = br.readLine();
        T = br.readLine();
        K = T.length();

        System.out.println(dfs(S, T));
    }

    public static int dfs(String s, String t) {
        if (s.length() == t.length()) {
            return s.equals(t) ? 1 : 0;
        }

        if (t.charAt(0) == 'B') {
            String reversed = new StringBuilder(t.substring(1)).reverse().toString();
            if (dfs(s, reversed) == 1) return 1;
        }

        if (t.charAt(t.length() - 1) == 'A') {
            if (dfs(s, t.substring(0, t.length() - 1)) == 1) return 1;
        }

        return 0;
    }
}
```
