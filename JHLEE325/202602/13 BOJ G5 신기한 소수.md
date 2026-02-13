```java
import java.io.*;
import java.util.*;

public class Main {
    
    static int N;
    static StringBuilder sb = new StringBuilder();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        dfs(2, 1);
        dfs(3, 1);
        dfs(5, 1);
        dfs(7, 1);

        System.out.print(sb.toString());
    }

    static void dfs(int num, int length) {
        if (length == N) {
            sb.append(num).append("\n");
            return;
        }

        for (int i = 1; i <= 9; i += 2) {
            int nextNum = num * 10 + i;
            if (isPrime(nextNum)) {
                dfs(nextNum, length + 1);
            }
        }
    }

    static boolean isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
}
```
