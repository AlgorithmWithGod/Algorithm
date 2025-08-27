```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    private static String S, T;
    private static boolean isFind = false;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        S = br.readLine();
        T = br.readLine();

        dfs(T);
        System.out.println(isFind ? 1 : 0);
    }

    private static void dfs(String cur) {
        if (isFind)
            return;
        if (cur.length() == S.length()) {
            if (cur.equals(S)) isFind = true;
            return;
        }

        // 마지막이 A라면 A 제거
        if (cur.charAt(cur.length() - 1) == 'A') {
            dfs(cur.substring(0, cur.length() - 1));
        }

        // 첫 글자가 B라면 B 제거 후 뒤집기
        if (cur.charAt(0) == 'B') {
            StringBuilder sb = new StringBuilder(cur.substring(1));
            dfs(sb.reverse().toString());
        }
    }
}

```
