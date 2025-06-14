```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] rows;
    static int[] cols;
    static int[][] dp;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        rows = new int[N+1];
        cols = new int[N+1];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            rows[i] = Integer.parseInt(st.nextToken());
            cols[i] = Integer.parseInt(st.nextToken());
        }
        dp = new int[N+1][N+1];

        for (int len = 2; len <= N; len++) { //구간
            for (int i = 1; i <= N - len + 1; i++) { //시작점
                int j = i + len - 1; //끝점
                dp[i][j] = Integer.MAX_VALUE;

                for (int k = i; k < j; k++) { //분할지점
                    int num = dp[i][k] + dp[k+1][j] + rows[i]*cols[k]*cols[j];
                    dp[i][j] = Math.min(dp[i][j], num);
                }
            }
        }
        bw.write(dp[1][N] + "\n");
        bw.close();
    }
}
```
