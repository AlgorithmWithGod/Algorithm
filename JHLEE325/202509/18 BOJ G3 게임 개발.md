```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[] buildTime;
    static List<Integer>[] require;
    static int[] dp;
    static boolean[] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        n = Integer.parseInt(br.readLine());
        buildTime = new int[n + 1];
        require = new ArrayList[n + 1];
        dp = new int[n + 1];
        visited = new boolean[n + 1];

        for (int i = 1; i <= n; i++) {
            require[i] = new ArrayList<>();
        }

        for (int i = 1; i <= n; i++) {
            st = new StringTokenizer(br.readLine());
            buildTime[i] = Integer.parseInt(st.nextToken());

            while (true) {
                int pre = Integer.parseInt(st.nextToken());
                if (pre == -1) break;
                require[i].add(pre);
            }
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= n; i++) {
            sb.append(dfs(i)).append("\n");
        }
        System.out.print(sb);
    }

    static int dfs(int i) {
        if (visited[i]) return dp[i];

        if (require[i].isEmpty()) {
            dp[i] = buildTime[i];
        } else {
            int maxPre = 0;
            for (int pre : require[i]) {
                maxPre = Math.max(maxPre, dfs(pre));
            }
            dp[i] = maxPre + buildTime[i];
        }

        visited[i] = true;
        return dp[i];
    }
}

```
