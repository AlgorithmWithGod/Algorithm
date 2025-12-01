```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dr = {-3, -3, 3, 3, -2, 2, -2, 2};
    private static final int[] dc = {-2, 2, -2, 2, -3, -3, 3, 3};
    private static final int[] check1r = {-1, -1, 1, 1, 0, 0, 0, 0};
    private static final int[] check1c = {0, 0, 0, 0, -1, -1, 1, 1};
    private static final int[] check2r = {-2, -2, 2, 2, -1, 1, -1, 1};
    private static final int[] check2c = {-1, 1, -1, 1, -2, -2, 2, 2};
    private static int R = 10;
    private static int C = 9;
    private static int r1, c1, r2, c2;
    private static int[][] dist;

    public static void main(String[] args) throws IOException {
        init();
        
        int result = bfs();
        bw.write(result + "\n");

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        r1 = Integer.parseInt(st.nextToken());
        c1 = Integer.parseInt(st.nextToken());
        
        st = new StringTokenizer(br.readLine());
        r2 = Integer.parseInt(st.nextToken());
        c2 = Integer.parseInt(st.nextToken());
        
        dist = new int[R][C];
        for (int i = 0; i < R; i++) {
            Arrays.fill(dist[i], -1);
        }
    }

    private static int bfs() {
        Queue<Node> q = new LinkedList<>();
        q.offer(new Node(r1, c1));
        dist[r1][c1] = 0;

        while (!q.isEmpty()) {
            Node cur = q.poll();
            
            if (cur.r == r2 && cur.c == c2) {
                return dist[cur.r][cur.c];
            }

            for (int i = 0; i < 8; i++) {
                int nr = cur.r + dr[i];
                int nc = cur.c + dc[i];

                if (OOB(nr, nc) || dist[nr][nc] != -1) continue;

                int t1r = cur.r + check1r[i];
                int t1c = cur.c + check1c[i];
                if (t1r == r2 && t1c == c2) continue;

                int t2r = cur.r + check2r[i];
                int t2c = cur.c + check2c[i];
                if (t2r == r2 && t2c == c2) continue;

                dist[nr][nc] = dist[cur.r][cur.c] + 1;
                q.offer(new Node(nr, nc));
            }
        }
        return -1;
    }
    
    private static boolean OOB(int nr, int nc) {
        return nr < 0 || nc < 0 || nr > R-1 || nc > C-1;
    }

    static class Node {
        int r, c;
        public Node(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }
}
```
