```java
import java.util.*;
import java.io.*;

public class boj29704 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int n;
    static int t;
    static int[] dp;

    public static void main(String[] args) throws Exception {
        nextLine();
        n = nextInt();
        t = nextInt();
        dp = new int[t+1];

        int all = 0;
        while (n-- > 0) {
            nextLine();
            int d = nextInt();
            int m = nextInt();
            all += m;

            for (int i = t; i >= 0; i--) {
                if (i < d) break;
                dp[i] = Math.max(dp[i], dp[i-d] +m);
            }
        }

        System.out.println(all - dp[t]);
    }
}
```
