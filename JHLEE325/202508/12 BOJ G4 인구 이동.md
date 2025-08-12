```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, l, r;
    static int[][] map;
    static boolean[][] visited;
    static int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    static List<int[]> union;
    static int unionSum;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        l = Integer.parseInt(st.nextToken());
        r = Integer.parseInt(st.nextToken());

        map = new int[n][n];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int days = 0;
        while (true) {
            visited = new boolean[n][n];
            boolean moved = false;

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (visited[i][j]) continue;

                    union = new ArrayList<>();
                    unionSum = 0;
                    bfs(new int[]{i, j});

                    if (union.size() > 1) {
                        moved = true;
                        int avg = unionSum / union.size();
                        for (int[] cell : union) {
                            map[cell[0]][cell[1]] = avg;
                        }
                    }
                }
            }

            if (!moved) break;
            days++;
        }

        System.out.println(days);
    }

    static void bfs(int[] start){
        ArrayDeque<int[]> q = new ArrayDeque<>();
        int sr = start[0], sc = start[1];

        visited[sr][sc] = true;
        q.add(new int[]{sr, sc});
        union.add(new int[]{sr, sc});
        unionSum += map[sr][sc];

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int cr = cur[0], cc = cur[1];

            for (int d = 0; d < 4; d++) {
                int nr = cr + dir[d][0];
                int nc = cc + dir[d][1];
                if (nr < 0 || nr >= n || nc < 0 || nc >= n) continue;
                if (visited[nr][nc]) continue;

                int diff = Math.abs(map[cr][cc] - map[nr][nc]);
                if (diff >= l && diff <= r) {
                    visited[nr][nc] = true;
                    q.add(new int[]{nr, nc});
                    union.add(new int[]{nr, nc});
                    unionSum += map[nr][nc];
                }
            }
        }
    }
}

```
