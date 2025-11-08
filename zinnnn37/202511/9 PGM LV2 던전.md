```java
public class PGM_LV2_피로도 {

    private static int N, ans;
    private static boolean[] visited;
    private static int[][]   dungeons;

    private static void init(int[][] d) {
        N = d.length;
        ans = 0;
        dungeons = d;
        visited = new boolean[N];
    }

    private static void sol(int depth, int stamina, int cnt) {
        ans = Math.max(ans, cnt);

        for (int i = 0; i < N; i++) {
            if (visited[i] || stamina < dungeons[i][0]) continue;

            visited[i] = true;
            sol(depth + 1, stamina - dungeons[i][1], cnt + 1);
            visited[i] = false;
        }
    }

    public int solution(int k, int[][] d) {
        init(d);
        sol(0, k, 0);

        return ans;
    }
}
```