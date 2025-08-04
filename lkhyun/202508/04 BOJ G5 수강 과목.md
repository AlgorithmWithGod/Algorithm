```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,K;
    static int[] prior;
    static int[] studyTime;
    static int[] dp;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        prior = new int[K];
        studyTime = new int[K];
        dp = new int[N+1];

        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());
            int I = Integer.parseInt(st.nextToken());
            int T = Integer.parseInt(st.nextToken());
            prior[i] = I;
            studyTime[i] = T;
        }

        for (int i = 0; i < K; i++) {
            for (int j = N; j >= studyTime[i]; j--) {
                dp[j] = Math.max(dp[j],dp[j-studyTime[i]]+prior[i]);
            }
        }
        bw.write(dp[N]+"");
        bw.close();
    }
}
```
