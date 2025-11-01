```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int[][] cost;
    static int[][] dp;
    static final int INF = 987654321;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        N = Integer.parseInt(br.readLine());
        cost = new int[N][N];
        
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        dp = new int[N][1 << N];
        for (int i = 0; i < N; i++) {
            Arrays.fill(dp[i], -1);
        }
        
        System.out.println(solve(0, 0));
    }
    
    static int solve(int person, int mask) {
        if (person == N) {
            return 0;
        }
        
        if (dp[person][mask] != -1) {
            return dp[person][mask];
        }
        
        int result = INF;
        
        for (int job = 0; job < N; job++) {
            if ((mask & (1 << job)) == 0) {
                int nextMask = mask | (1 << job);
                result = Math.min(result, cost[person][job] + solve(person + 1, nextMask));
            }
        }
        
        return dp[person][mask] = result;
    }
}
```
