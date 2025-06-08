```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int N;
    static int[][] map, dp;
    static final int MAX_VALUE = 16_000_001;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        
        N = Integer.parseInt(br.readLine());
        map = new int[N][N];
        dp = new int[N][(1<<N) - 1];
        for(int i = 0; i < N; i++) Arrays.fill(dp[i], -1);

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = nextInt(st);
            }
        }

        System.out.println(dfs(0, 1));
    }

    static int dfs(int now, int visited) {
        if (visited == (1 << N) - 1) {
            if (map[now][0] == 0) return MAX_VALUE;
            return map[now][0];
        }

        if(dp[now][visited] != -1) return dp[now][visited];
        dp[now][visited] = MAX_VALUE;

        for (int i = 0; i < N; i++) {
            if((visited & (1 << i)) == 0 && map[now][i] != 0) {
                dp[now][visited] = Math.min(dfs(i, visited | (1 << i)) + map[now][i], dp[now][visited]);
            }
        }

        return dp[now][visited];
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
