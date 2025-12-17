```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        int[] start = {2, 3, 5, 7};
        for (int s : start) dfs(s, 1);

        System.out.print(sb);
    }
    
    static boolean isPrime(int x) {
        if (x < 2) return false;
        if (x == 2) return true;
        if (x % 2 == 0) return false;
        for (int i = 3; i * i <= x; i += 2) {
            if (x % i == 0) return false;
        }
        return true;
    }

    static void dfs(int num, int depth) {
        if (depth == N) {
            sb.append(num).append('\n');
            return;
        }
        for (int d = 1; d <= 9; d++) {
            int next = num * 10 + d;
            if (isPrime(next)) dfs(next, depth + 1);
        }
    }
}
```
