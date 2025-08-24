```import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]>[] d;
    private static int[][] map;
    private static boolean[][] visited;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();

        bw.write(BFS(1, 1) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());

        map = new int[N+1][M+1];
        visited = new boolean[N+1][M+1];
        d = new List[1000001];

        for (int i = 0; i < 1000001; i++) {
            d[i] = new ArrayList<>();
        }

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static String BFS(int x, int y) {
        Queue<int[]> q = new ArrayDeque<>();
        visited[x][y] = true;
        q.add(new int[] {x, y});

        while (!q.isEmpty()) {
            int[] current = q.poll();
            if (current[0] == N && current[1] == M) {
                return "yes";
            }

            if (d[map[current[0]][current[1]]].size() == 0) {
                findFactor(map[current[0]][current[1]]);
            }

            for (int[] element : d[map[current[0]][current[1]]]) {
                for (int i = 0; i < element.length; i++) {
                    int nx = element[i];
                    int ny = element[i^1];

                    if (OOB(nx, ny) || visited[nx][ny]) continue;
                    visited[nx][ny] = true;
                    q.add(new int[] {nx, ny});
                }
            }
        }

        return "no";
    }

    private static void findFactor(int n) {
        for (int i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                d[n].add(new int[] {i, n / i});
            }
        }
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 1 || nx > N || ny < 1 || ny > M;
    }
}

```
