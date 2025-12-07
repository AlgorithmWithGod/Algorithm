```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_G5_상범_빌딩 {

    private static final int[] dx = { 0, 1, 0, -1, 0, 0 };
    private static final int[] dy = { 1, 0, -1, 0, 0, 0 };
    private static final int[] dz = { 0, 0, 0, 0, 1, -1 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int L, R, C; // 층 행 열
    private static char[][][]    building;
    private static boolean[][][] visited;
    private static Queue<Node>   q;

    private static class Node {
        int floor;
        int x;
        int y;
        int cnt;

        Node(int floor, int x, int y, int cnt) {
            this.floor = floor;
            this.x = x;
            this.y = y;
            this.cnt = cnt;
        }

    }

    public static void main(String[] args) throws IOException {
        while (init()) {
            sol();
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean init() throws IOException {
        st = new StringTokenizer(br.readLine());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        if (L == 0) return false;

        building = new char[L][R][C];
        visited = new boolean[L][R][C];
        q = new ArrayDeque<>();
        for (int i = 0; i < L; i++) {
            for (int j = 0; j < R; j++) {
                String line = br.readLine();
                for (int k = 0; k < C; k++) {
                    building[i][j][k] = line.charAt(k);

                    if (building[i][j][k] == 'S') {
                        q.offer(new Node(i, j, k, 0));
                        visited[i][j][k] = true;
                    }
                }
            }
            br.readLine();
        }
        return true;
    }

    private static void sol() {
        while (!q.isEmpty()) {
            Node cur = q.poll();

            if (building[cur.floor][cur.x][cur.y] == 'E') {
                sb.append("Escaped in ").append(cur.cnt).append(" minute(s).\n");
                return;
            }

            for (int d = 0; d < 6; d++) {
                int nz = cur.floor + dz[d];
                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                if (OOB(nz, nx, ny) || visited[nz][nx][ny] || building[nz][nx][ny] == '#') continue;

                q.offer(new Node(nz, nx, ny, cur.cnt + 1));
                visited[nz][nx][ny] = true;
            }
        }
        sb.append("Trapped!\n");
    }

    private static boolean OOB(int floor, int x, int y) {
        return floor < 0 || L <= floor || x < 0 || R <= x || y < 0 || C <= y;
    }

}
```