```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N;
    static int[][] forest;
    static int[][] dp;
    
    // 상하좌우
    static int[] di = {-1, 1, 0, 0};
    static int[] dj = {0, 0, -1, 1};

    static int ans = 0;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());

        forest = new int[N][N];
        dp = new int[N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                forest[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                ans = Math.max(ans, DFS(i, j));
            }
        }
        
        bw.write(ans + "");
        bw.close();
    }

    public static int DFS(int i, int j) {
        if (dp[i][j] != 0) {
            return dp[i][j];
        }
        
        dp[i][j] = 1;
        
        for (int k = 0; k < 4; k++) {
            int ni = i + di[k];
            int nj = j + dj[k];
            
            if (ni >= 0 && ni < N && nj >= 0 && nj < N && forest[ni][nj] > forest[i][j]) {
                dp[i][j] = Math.max(dp[i][j], DFS(ni, nj) + 1);
            }
        }
        
        return dp[i][j];
    }
}
```
