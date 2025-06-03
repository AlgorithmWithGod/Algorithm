```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[][] dp;
    static int N,M;
    static int[] arr;
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N+1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        dp = new int[N+1][N+1];
        for (int i = 1; i <= N; i++) {
            dp[i][i] = 1;
        }
        for (int i = 1; i < N; i++) {
            if(arr[i] == arr[i+1]){
                dp[i][i+1] = 1;
            }
        }
        for (int i = 2; i < N; i++) {
            for (int j = 1; j+i <= N; j++) {
                if(arr[j] == arr[j+i]){
                    dp[j][j+i] = dp[j+1][j+i-1];
                }else{
                    dp[j][j+i] = 0;
                }
            }
        }
        M = Integer.parseInt(br.readLine());
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int S = Integer.parseInt(st.nextToken());
            int E = Integer.parseInt(st.nextToken());
            bw.write(dp[S][E] + "\n");
        }
        bw.close();
    }
}

```
