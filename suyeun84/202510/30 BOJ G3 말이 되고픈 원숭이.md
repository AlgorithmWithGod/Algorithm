```java
import java.io.*;
import java.util.*;

public class boj1600 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int[][] dir = new int[][] {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};
    static int[][] hdir = new int[][] {{-2, -1}, {-1, -2}, {1, -2}, {2, -1}, {-2, 1}, {-1, 2}, {1, 2}, {2, 1}};
    static int K, W, H;
    static int[][] board;
    static boolean[][][] visited;
    public static void main(String[] args) throws Exception {
        nextLine();
        K = nextInt();
        nextLine();
        W = nextInt();
        H = nextInt();
        board = new int[H][W];
        visited = new boolean[H][W][K+1];
        for (int i = 0; i < H; i++) {
            nextLine();
            for (int j = 0; j < W; j++) {
                board[i][j] = nextInt();
            }
        }
        bfs();
    }

    static void bfs() {
        Queue<Move> q = new LinkedList<>();
        q.add(new Move(0, 0, 0, 0));
        visited[0][0][0] = true;
        
        while (!q.isEmpty()) {
            Move cur = q.poll();
            if (cur.y == H-1 && cur.x == W-1) {
                System.out.println(cur.dep);
                return;
            }
            
            for (int[] d : dir) {
                int ny = cur.y + d[0];
                int nx = cur.x + d[1];
                if (ny >= H || ny < 0 || nx >= W || nx < 0 || board[ny][nx] == 1) continue;
                
                if (!visited[ny][nx][cur.horse]) {
                	visited[ny][nx][cur.horse] = true;
                	q.offer(new Move(ny, nx, cur.horse, cur.dep + 1));
                }
            }
            if (cur.horse < K) {
            	for (int[] d : hdir) {
            		int ny = cur.y + d[0];
                    int nx = cur.x + d[1];
                    if (ny >= H || ny < 0 || nx >= W || nx < 0 || board[ny][nx] == 1) continue;
                    if (!visited[ny][nx][cur.horse+1]) {
                    	visited[ny][nx][cur.horse+1] = true;
                    	q.offer(new Move(ny, nx, cur.horse+1, cur.dep + 1));
                    }
            	}
            }
        }
        System.out.println(-1);
    }

    static class Move {
        int y, x, horse, dep;
        public Move(int y, int x, int horse, int dep) {
            this.y = y;
            this.x = x;
            this.horse = horse;
            this.dep = dep;
        }
    }
}
```
