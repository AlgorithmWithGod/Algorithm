```java
import java.io.*;
import java.util.*;

public class boj4781 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }
    static double nextDouble() { return Double.parseDouble(st.nextToken()); }

    public static void main(String[] args) throws Exception {
        while(true) {
            nextLine();
            int n = nextInt(); // 사탕 종류의 수
            int m = (int) (nextDouble() * 100); // 상근이 돈 양
            if (n == 0 && m == 0) break;
            Candy[] candy = new Candy[n+1];
            for (int i = 1; i <= n; i++) {
                nextLine();
                candy[i] = new Candy(nextInt(), (int) (nextDouble() * 100 + 0.5));
            }
            System.out.println(solve(n, m, candy));
        }
    }

    static private int solve(int n, int m, Candy[] candy) {
        int[] dp = new int[m+1];
        for (int i = 1; i <= n; i++) { // 사탕 종류
            int cal = candy[i].c;
            int val = candy[i].p;
            for (int j = 0; j <= m; j++) {
                if (j - val >= 0) dp[j] = Math.max(dp[j], dp[j-val] + cal);
            }
        }
        return dp[m];
    }

    static class Candy {
        int c;
        int p;
        public Candy(int c, int p) {
            this.c = c;
            this.p = p;
        }
    }
}
```
