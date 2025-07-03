```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int T;
    static int N,M;
    static long[][] dp;
    static long count;

    public static void main(String[] args) throws Exception{
        T = Integer.parseInt(br.readLine());
        N = Integer.parseInt(br.readLine());
        int[] A = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(st.nextToken());
        }

        M = Integer.parseInt(br.readLine());
        int[] B = new int[M];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            B[i] = Integer.parseInt(st.nextToken());
        }

        dp = new long[N][N];
        Map<Long,Integer> m = new HashMap<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; i+j < N; j++) {
                if(i == 0){
                    dp[j][j] = A[j];
                }else{
                    dp[j][i+j] = dp[j][i+j-1] + A[i+j];
                }
                long target = T - dp[j][i+j];
                m.put(target, m.getOrDefault(target,0)+1);
            }
        }

        count = 0;
        dp = new long[M][M];
        for (int i = 0; i < M; i++) {
            for (int j = 0; i+j < M; j++) {
                if(i == 0){
                    dp[j][j] = B[j];
                }else{
                    dp[j][i+j] = dp[j][i+j-1] + B[i+j];
                }
                Integer target = m.get(dp[j][i+j]);
                if(target != null){
                    count += target;
                }
            }
        }

        bw.write(count + "");
        bw.close();
    }

}
```
