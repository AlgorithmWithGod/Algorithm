```java
import java.io.*;
import java.util.*;

public class boj9764 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int T = nextInt();
        int[] arr = new int[T];
        int max = 0;
        for (int i = 0; i < T; i++) {
            nextLine();
            arr[i] = nextInt();
            max = Math.max(max, arr[i]);
        }
        int mod = 100999;
        int[] dp = new int[max + 1];
        dp[0] = 1;

        for (int k = 1; k <= max; k++) {
            for (int i = max; i >= k; i--) {
                dp[i] = (dp[i] + dp[i - k]) % mod;
            }
        }
        for (int i = 0; i < T; i++) System.out.println(dp[arr[i]]);
    }
}
```
