```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {0, 1, 0, -1, 0};
    private static final int[] dy = {1, 0, -1, 0, 0};
    private static Map<String, Integer> ghosts;
    private static boolean[][][] visited;
    private static char[][] map;
    private static int[] start, end;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        if (answer == -1) bw.write("GG");
        else bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        start = new int[2];
        end = new int[2];

        start[0] = Integer.parseInt(st.nextToken())-1;
        start[1] = Integer.parseInt(st.nextToken())-1;
        end[0] = Integer.parseInt(st.nextToken())-1;
        end[1] = Integer.parseInt(st.nextToken())-1;

        map = new char[N][M];
        ghosts = new HashMap<>();
        visited = new boolean[N][M][4];

        for (int i = 0; i < N; i++) {
            map[i] = br.readLine().toCharArray();
            for (int j = 0; j < M; j++) {
                if (map[i][j] != '.' && map[i][j] != '#') {
                    ghosts.put(i+","+j, map[i][j] - '0');
                }
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        visited[start[0]][start[1]][0] = true;
        q.add(new int[]{start[0], start[1], 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == end[0] && current[1] == end[1]) return current[2];

            for (int i = 0; i < 5; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] != '.' || visited[nx][ny][(current[2]+1)%4] || find(nx, ny, current[2]+1)) continue;
                visited[nx][ny][(current[2]+1)%4] = true;
                q.add(new int[]{nx, ny, current[2]+1});
            }
        }

        return -1;
    }

    private static boolean find(int nx, int ny, int nTime) {
        for (int i = 0; i < 4; i++) {
            int nnx = nx;
            int nny = ny;
            int d = 0;
            while (!OOB(nnx, nny)) {
                if (map[nnx][nny] == '#') break;
                else if (map[nnx][nny] != '.') {
                    int nState = (map[nnx][nny] - '0' + nTime) % 4;
                    if (Math.abs(i-nState) == 2) {
                        return true;
                    }
                    break;
                }
                d++;
                nnx = nx + dx[i]*d;
                nny = ny + dy[i]*d;
            }
        }

        return false;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > M-1;
    }
}
```
