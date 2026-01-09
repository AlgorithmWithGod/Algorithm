```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static List<Integer>[] adjList;
    static StringTokenizer st;
    static int[][] dp;
    static boolean[] visited;
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        adjList = new ArrayList[N+1];
        for (int i = 0; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }
        dp = new int[N+1][2];
        visited = new boolean[N+1];

        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            adjList[u].add(v);
            adjList[v].add(u);
        }
        dfs(1);
        System.out.println(Math.min(dp[1][0],dp[1][1]));
    }
    public static void dfs(int cur){
        visited[cur] = true;
        dp[cur][1] = 1;

        for (int next : adjList[cur]) {
            if(visited[next]) continue;
            dfs(next);
            dp[cur][0] += dp[next][1];
            dp[cur][1] += Math.min(dp[next][0],dp[next][1]);
        }
    }
}
```
