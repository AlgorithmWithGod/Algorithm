```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m, res;
    static int[][] map;
    static boolean[][] visited;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        map = new int[n + 2][m + 2];

        for (int i = 1; i <= n; i++) {
            String s = br.readLine();
            for (int j = 1; j <= m; j++) {
                map[i][j] = Integer.parseInt(String.valueOf(s.charAt(j-1)));
            }
        }

        for (int k = 2; k <= 9; k++) {
            visited = new boolean[n + 2][m + 2];
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= m; j++) {
                    if(visited[i][j]||map[i][j]>=k)
                        continue;
                    res += bfs(i, j, k);
                }
            }
        }
        System.out.println(res);
    }

    static int bfs(int x, int y, int height) {
        Queue<int[]> q = new ArrayDeque<>();
        List<int[]> list = new ArrayList<>();
        boolean ground = false;
        int water = 0;
        q.add(new int[]{x, y});
        list.add(new int[]{x, y});

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            for (int d = 0; d < 4; d++) {
                int nx = cur[0] + dx[d];
                int ny = cur[1] + dy[d];
                if (map[nx][ny] == 0) {
                    ground=true;
                    continue;
                }
                if (!visited[nx][ny] && map[nx][ny] < height) {
                    q.add(new int[]{nx, ny});
                    list.add(new int[]{nx, ny});
                    visited[nx][ny] = true;
                }
            }
        }
        if(ground)
            return 0;

        for (int[] pool : list) {
            water += height - map[pool[0]][pool[1]];
            map[pool[0]][pool[1]] = height;
        }
        return water;
    }
}
```
