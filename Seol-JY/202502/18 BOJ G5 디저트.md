```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static int M;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = nextInt(st);
        M = nextInt(st);
        int[][] arr = new int[M][N];
        int[][] dp = new int[M][N];
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                arr[i][j] = nextInt(st);
                if (j == 0) {
                    dp[i][0] = arr[i][j];
                }
            }
        }
        for (int i = 1; i < N; i++) {
            for (int j = 0; j < M; j++) {
                int max = Integer.MIN_VALUE;
                for (int k = 0; k < M; k++) {
                    if (k == j) max = Math.max(max, dp[k][i-1] + arr[j][i]/2);
                    else max = Math.max(max, dp[k][i-1] + arr[j][i]);
                }
                dp[j][i] = max;
            }
        }

        int answer = Integer.MIN_VALUE;
        for (int i = 0; i < M; i++) {
            answer = Math.max(answer, dp[i][N-1]);
        }
        System.out.println(answer);
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```

