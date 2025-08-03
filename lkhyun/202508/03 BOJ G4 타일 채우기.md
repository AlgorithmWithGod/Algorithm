```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] dp;

    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        if(N%2 == 1){
            bw.write("0");
            bw.close();
            return;
        }

        dp = new int[N+1];
        dp[0] = 1;
        dp[2] = 3;
        for (int i = 4; i <= N; i++) {
            dp[i] = 4*dp[i-2] - dp[i-4];
        }
        bw.write(dp[N]+"");
        bw.close();
    }
}
```
