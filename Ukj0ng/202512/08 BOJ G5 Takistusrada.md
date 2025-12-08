```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dvx = {0, 0, 0, 1, -1};
    private static final int[] dvy = {0, 1, -1, 0, 0};
    private static final int OFFSET = 50;
    private static final int MAX_COORD = 100;
    private static final int MAX_V = 7;
    private static final int V_OFFSET = 7;
    private static int targetX, targetY;
    private static int N;
    private static boolean[][] isObstacle;
    private static boolean[][][][] visited;

    public static void main(String[] args) throws IOException {
        init();
        int result = BFS();

        bw.write(String.valueOf(result));
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        targetX = Integer.parseInt(st.nextToken());
        targetY = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());

        isObstacle = new boolean[MAX_COORD + 1][MAX_COORD + 1];
        visited = new boolean[MAX_COORD + 1][MAX_COORD + 1][16][16];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int ox = Integer.parseInt(st.nextToken());
            int oy = Integer.parseInt(st.nextToken());
            
            if (!OOB(ox + OFFSET, oy + OFFSET)) {
                isObstacle[ox + OFFSET][oy + OFFSET] = true;
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();

        int startX = 0 + OFFSET;
        int startY = 0 + OFFSET;
        int startVx = 0 + V_OFFSET;
        int startVy = 0 + V_OFFSET;

        q.add(new int[] {startX, startY, startVx, startVy, 0});
        visited[startX][startY][startVx][startVy] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int cx = cur[0];
            int cy = cur[1];
            int cvx = cur[2];
            int cvy = cur[3];
            int time = cur[4];
            
            if (cx - OFFSET == targetX && cy - OFFSET == targetY) {
                return time;
            }

            int realVx = cvx - V_OFFSET;
            int realVy = cvy - V_OFFSET;
            
            for (int i = 0; i < 5; i++) {
                int nRealVx = realVx + dvx[i];
                int nRealVy = realVy + dvy[i];
                
                if (Math.abs(nRealVx) > MAX_V || Math.abs(nRealVy) > MAX_V) continue;

                int nx = cx + nRealVx;
                int ny = cy + nRealVy;
                int nvx = nRealVx + V_OFFSET;
                int nvy = nRealVy + V_OFFSET;
                
                if (OOB(nx, ny) || visited[nx][ny][nvx][nvy] || hasCollision(cx, cy, nx, ny)) continue;
                visited[nx][ny][nvx][nvy] = true;
                q.add(new int[] {nx, ny, nvx, nvy, time + 1});
            }
        }

        return -1; 
    }

    private static boolean hasCollision(int x1, int y1, int x2, int y2) {
        int dx = x2 - x1;
        int dy = y2 - y1;
        
        if (dx == 0 && dy == 0) {
            return isObstacle[x2][y2];
        }
        
        int steps = gcd(Math.abs(dx), Math.abs(dy));

        int stepX = dx / steps;
        int stepY = dy / steps;

        for (int i = 1; i <= steps; i++) {
            int checkX = x1 + stepX * i;
            int checkY = y1 + stepY * i;

            if (isObstacle[checkX][checkY]) return true;
        }

        return false;
    }

    private static int gcd(int a, int b) {
        while (b != 0) {
            int r = a % b;
            a = b;
            b = r;
        }
        return a;
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || x > MAX_COORD || y < 0 || y > MAX_COORD;
    }
}
```
