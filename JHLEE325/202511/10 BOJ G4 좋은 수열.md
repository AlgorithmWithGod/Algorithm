```java
import java.io.*;
public class Main {
    static int N;
    static boolean found = false;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine().trim());
        dfs("", 0);
    }

    static void dfs(String s, int depth) {
        if (found) return;
        if (depth == N) {
            System.out.println(s);
            found = true;
            return;
        }
        for (int i = 1; i <= 3; i++) {
            String ns = s + i;
            if (goodString(ns)) {
                dfs(ns, depth + 1);
            }
            if (found) return;
        }
    }

    static boolean goodString(String s) {
        int len = s.length();
        for (int l = 1; l <= len / 2; l++) {
            String a = s.substring(len - 2*l, len - l);
            String b = s.substring(len - l, len);
            if (a.equals(b)) {
                return false;
            }
        }
        return true;
    }
}
```
