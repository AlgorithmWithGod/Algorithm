```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M,K;
    static int[] candies;
    static List<Integer>[] friends;
    static int[] dp;

    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        candies = new int[N+1];
        friends = new List[N+1];
        dp = new int[K];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            candies[i] = Integer.parseInt(st.nextToken());
            friends[i] = new ArrayList<>();
        }

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            friends[u].add(v);
            friends[v].add(u);
        }

        boolean[] visited = new boolean[N+1];
        for (int i = 1; i <= N; i++) {
            if(visited[i]) continue;
            int childCnt = 0;
            int candyCnt = 0;

            ArrayDeque<Integer> q = new ArrayDeque<>();
            q.add(i);
            visited[i] = true;
            while (!q.isEmpty()) {
                int u = q.poll();
                childCnt++;
                candyCnt += candies[u];
                for (int v : friends[u]) {
                    if(!visited[v]) {
                        q.add(v);
                        visited[v] = true;
                    }
                }
            }

            for (int j = K-1; j >= childCnt; j--) {
                dp[j] = Math.max(dp[j],dp[j-childCnt] + candyCnt);
            }
        }

        int maxCnt = 0;
        for (int i = 0; i < K; i++) {
            maxCnt = Math.max(maxCnt, dp[i]);
        }
        bw.write(maxCnt + "");

        bw.close();
    }
}
```
