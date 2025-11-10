```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class PGM_LV2_전력망_둘로_나누기 {

    private static int N, ans;
    private static int[][] wires;
    private static boolean[] visited;
    private static List<Integer>[] graph;

    private static void init(int n, int[][] wire) {
        N = n;
        ans = Integer.MAX_VALUE;
        wires = wire;

        visited = new boolean[N + 1];

        graph = new List[N + 1];
        for (int i = 0; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int[] edge : wires) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }
    }

    private static void sol() {
        int cnt;
        int left;
        for (int i = 0; i < N - 1; i++) {
            Arrays.fill(visited, false);

            visited[wires[i][0]] = true;
            visited[wires[i][1]] = true;

            cnt = exclude(wires[i][0], wires[i]);

            left = N - cnt;
            ans = Math.min(ans, Math.abs(cnt - left));
        }
    }

    private static int exclude(int start, int[] target) {
        int cnt = 0;

        for (int n : graph[start]) {
            if (visited[n]) continue;

            visited[n] = true;
            cnt += exclude(n, target);
        }
        return cnt + 1;
    }

    public int solution(int n, int[][] wires) {
        init(n, wires);
        sol();
        return ans;
    }

}
```