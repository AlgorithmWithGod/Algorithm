```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_2533_사회망_서비스_SNS {

    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N;
    private static int[][] dp;  // [노드][0(일반인)/1(얼리어답터)]

    private static boolean[] visited;
    private static List<Integer>[] tree;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        tree = new List[N + 1];
        for (int i = 1; i <= N; i++) {
            tree[i] = new ArrayList<>();
        }

        for (int i = 0; i < N - 1; i++) {
            st = new StringTokenizer(br.readLine());

            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());

            tree[u].add(v);
            tree[v].add(u);
        }
        visited = new boolean[N + 1];
        dp = new int[N + 1][2];
    }

    private static void sol() throws IOException {
        find(1);

        bw.write(Math.min(dp[1][0], dp[1][1]) + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void find(int u) {
        visited[u] = true;
        dp[u][0] = 1; // 초기화: 필요한 얼리어답터 수 = 1

        for (int v : tree[u]) {
            if (visited[v]) {
                continue;
            }
            find(v);
            dp[u][1] += dp[v][0]; // 내가 얼리어답터면 친구가 얼리어답터일 필요 없음
            dp[u][0] += Math.min(dp[v][0], dp[v][1]);
        }
    }

}
```