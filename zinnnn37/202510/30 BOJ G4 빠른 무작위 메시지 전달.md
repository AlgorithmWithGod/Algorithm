```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_25835_빠른_무작위_메시지_전달 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int ans;
    private static int[][] friends;
    private static boolean[] visited;

    public static void main(String[] args) throws IOException {
        init();
        sol();

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        ans = Integer.MAX_VALUE;

        friends = new int[12][12];
        for (int i = 0; i < 12; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 12; j++) {
                friends[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        visited = new boolean[6];
    }

    private static void sol() throws IOException {
        for (int nextGroup = 0; nextGroup < 6; nextGroup++) {
            int next = nextGroup * 2;

            visited[nextGroup] = true;
            dfs(1, next + 1, friends[next][next + 1]);
            dfs(1, next, friends[next + 1][next]);
            visited[nextGroup] = false;
        }
    }

    private static void dfs(int depth, int cur, int sum) throws IOException {
        if (depth == 6) {
            ans = Math.min(ans, sum);
            return;
        }

        for (int i = 0; i < 6; i++) {
            if (visited[i]) continue;

            int next = i * 2;

            visited[i] = true;
            dfs(depth + 1, next, sum + friends[cur][next + 1] + friends[next + 1][next]);
            dfs(depth + 1, next + 1, sum + friends[cur][next] + friends[next][next + 1]);
            visited[i] = false;
        }
    }

}
```