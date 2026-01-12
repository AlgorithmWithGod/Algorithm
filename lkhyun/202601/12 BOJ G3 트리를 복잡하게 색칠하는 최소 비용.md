```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static List<Integer>[] adjList;
    static long[][] dp;
    static int[] whiteCost;
    static int[] blackCost;
    static StringTokenizer st;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        adjList = new List[N];
        for (int i = 0; i < N; i++) {
            adjList[i] = new ArrayList<>();
        }
        dp = new long[N][2];
        whiteCost = new int[N];
        blackCost = new int[N];

        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            adjList[from].add(to);
        }

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            whiteCost[i] = Integer.parseInt(st.nextToken());
            blackCost[i] = Integer.parseInt(st.nextToken());
        }

        dfs(0);
        System.out.println(Math.min(dp[0][0],dp[0][1]));
    }
    public static void dfs(int cur){
        dp[cur][0] = whiteCost[cur];
        dp[cur][1] = blackCost[cur];
        for (Integer next : adjList[cur]) {
            dfs(next);
            dp[cur][0] += Math.min(dp[next][0],dp[next][1]);
            dp[cur][1] += dp[next][0];
        }
    }
}
```
