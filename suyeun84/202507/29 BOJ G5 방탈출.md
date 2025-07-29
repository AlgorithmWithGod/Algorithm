```java
import java.util.*;
import java.io.*;

public class boj23352 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N, M, answer, dep;
    static int[][] map;
    static int[][] dir = {{1,0}, {0,1}, {0,-1}, {-1,0}};
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        map = new int[N][M];
        answer = 0;
        dep = 0;
        for (int i = 0; i < N; i++) {
            nextLine();
            for (int j = 0; j < M; j++) map[i][j] = nextInt();
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 0) continue;
                bfs(i, j);
            }
        }
        System.out.println(answer);
    }

    static void bfs(int y, int x) {
        boolean[][] visited = new boolean[N][M];
        Queue<Pos> q = new LinkedList<>();
        q.add(new Pos(y, x, 0));
        visited[y][x] = true;

        while (!q.isEmpty()) {
            Pos curr = q.poll();
            boolean flag = true;

            for (int[] d : dir) {
                int ny = curr.y + d[0];
                int nx = curr.x + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M || visited[ny][nx] || map[ny][nx] == 0) continue;
                visited[ny][nx] = true;
                flag = false;
                q.add(new Pos(ny, nx, curr.cnt+1));
            }
            if (flag) {
                if (dep < curr.cnt) {
                    dep = curr.cnt;
                    answer = map[y][x] + map[curr.y][curr.x];
                } else if (dep == curr.cnt) {
                    answer = Math.max(answer, map[y][x] + map[curr.y][curr.x]);
                }
            }
        }
    }
}

class Pos {
    int y, x, cnt;
    public Pos(int y, int x, int cnt) {
        this.y = y;
        this.x = x;
        this.cnt = cnt;
    }
}
```
