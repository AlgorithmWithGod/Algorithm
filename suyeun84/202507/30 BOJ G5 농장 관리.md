```java
import java.util.*;
import java.io.*;

public class boj1245 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N, M, answer;
    static int[][] map;
    static boolean[][] visited, top;
    static int[][] dir = {{1,0}, {0,1}, {0,-1}, {-1,0}, {-1,1}, {-1,-1}, {1,1}, {1,-1}};
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        map = new int[N][M];
        top = new boolean[N][M];
        for (int i = 0; i < N; i++) {
            nextLine();
            for (int j = 0; j < M; j++) map[i][j] = nextInt();
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 0 || top[i][j]) continue;
                bfs(i, j);
            }
        }
        System.out.println(answer);
    }
    static void bfs(int y, int x) {
        Queue<Pos> q = new LinkedList<>();
        boolean[][] visited = new boolean[N][M];
        LinkedList<Pos> topList = new LinkedList<>();
        q.add(new Pos(y, x));
        visited[y][x] = true;
        while (!q.isEmpty()) {
            Pos cur = q.poll();
            for (int[] d : dir) {
                int ny = cur.y + d[0];
                int nx = cur.x + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M || visited[ny][nx]) continue;
                visited[ny][nx] = true;
                if (map[ny][nx] > map[cur.y][cur.x]) return;
                else if (map[ny][nx] == map[cur.y][cur.x]) {
                    q.add(new Pos(ny, nx));
                    topList.add(new Pos(ny, nx));
                }
            }
        }
        for (Pos pos : topList) {
            top[pos.y][pos.x] = true;
        }
        answer++;
    }

    static class Pos {
        int y, x;
        public Pos(int y, int x) {
            this.y = y;
            this.x = x;
        }
    }
}
```
