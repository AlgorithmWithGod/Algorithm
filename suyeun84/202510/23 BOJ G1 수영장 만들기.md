```java
import java.io.*;
import java.util.*;

public class boj1113 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    static int[][] dir = new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}};
    static int N, M, answer;
    static int[][] land;
    static boolean[][] visited;
    static Queue<int[]> q = new LinkedList<>();
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        answer = 0;
        land = new int[N][M];
        visited = new boolean[N][M];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                land[i][j] = Integer.parseInt(line.substring(j, j+1));
                min = Math.min(min, land[i][j]);
                max = Math.max(max, land[i][j]);
            }
        }
        for (int h = min; h < max; h++) {
            for (int i = 1; i < N-1; i++) {
                for (int j = 1; j < M-1; j++) {
                    if (land[i][j] == h) {
                        answer += bfs(i, j, h);
                    }
                }
            }
        }
        System.out.println(answer);
    }

    static int bfs(int y, int x, int h) {
        q.clear();
        q.add(new int[] {y, x});
        int cnt = 1;
        boolean flag = true;
        land[y][x] = h + 1;
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            for (int[] d : dir) {
                int ny = cur[0] + d[0];
                int nx = cur[1] + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M || land[ny][nx] < h) {
                    flag = false;
                    continue;
                }
                if (h != land[ny][nx]) continue;
                land[ny][nx] = h + 1;
                cnt++;
                q.offer(new int[] {ny, nx});
            }
        }
        if (flag) return cnt;
        return 0;
    }
}
```
