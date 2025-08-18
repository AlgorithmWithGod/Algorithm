```java
import java.util.*;
import java.io.*;

public class boj2636 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N, M, time = 0, answer = 0;
    static int[][] map;
    static int[][] dir = new int[][]{{1,0}, {-1,0}, {0,1}, {0,-1}};
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        map = new int[N][M];
        for (int i = 0; i < N; i++) {
            nextLine();
            for (int j = 0; j < M; j++) {
                map[i][j] = nextInt();
                if (map[i][j] == 1) answer++;
            }
        }
        while (answer > 0) {
            time++;
            int melted = solve();
            if (answer - melted == 0) break;
            answer -= melted;
        }
        System.out.println(time);
        System.out.println(answer);
    }
    // 밖이랑 연결되어 있는지 확인
    static int solve() {
        Queue<int[]> q = new LinkedList<>();
        boolean[][] visited = new boolean[N][M];
        q.add(new int[]{0, 0});
        int melted = 0;
        visited[0][0] = true;
        while(!q.isEmpty()) {
            int[] cur = q.poll();
            for (int[] d : dir) {
                int ny = cur[0] + d[0];
                int nx = cur[1] + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M || visited[ny][nx]) continue;
                if (map[ny][nx] == 0) {
                    visited[ny][nx] = true;
                    q.add(new int[] {ny, nx});
                } else {
                    map[ny][nx] = 0;
                    visited[ny][nx] = true;
                    melted++;
                }
            }
        }
        return melted;
    }
}
```
