```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {0, -1, 0, 1};
    private static final int[] dy = {-1, 0, 1, 0};
    private static Map<Integer, Integer> rooms;
    private static Set<Integer>[] near;
    private static int[][] arr;
    private static boolean[][] visited;
    private static boolean[][][] wall;
    private static int N, M, answer1, answer2, answer3;

    public static void main(String[] args) throws IOException {
        init();

        int num = 1;

        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                if (!visited[i][j]) {
                    BFS(i, j, num++);
                }
            }
        }

        near = new Set[rooms.size()+1];

        for (int i = 1; i <= rooms.size(); i++) {
            near[i] = new HashSet<>();
        }

        for (int i = 0; i < M; i++) {
            Arrays.fill(visited[i], false);
        }

        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                if (!visited[i][j]) {
                    setNear(i, j, arr[i][j]);
                }
            }
        }

        answer1 = rooms.size();
        for (int key : rooms.keySet()) {
            answer2 = Math.max(answer2, rooms.get(key));
        }

        for (int i = 1; i <= answer1; i++) {
            for (int e : near[i]) {
                answer3 = Math.max(answer3, rooms.get(i)+rooms.get(e));
            }
        }

        bw.write(answer1 + "\n" + answer2 + "\n" + answer3);
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st =  new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        arr = new int[M][N];
        visited = new boolean[M][N];
        wall = new boolean[M][N][4];

        rooms = new HashMap<>();

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                int temp = Integer.parseInt(st.nextToken());

                if (temp >= 8) {
                    temp -= 8;
                    wall[i][j][3] = true;
                }

                if (temp >= 4) {
                    temp -= 4;
                    wall[i][j][2] = true;
                }

                if (temp >= 2) {
                    temp -= 2;
                    wall[i][j][1] = true;
                }

                if (temp >= 1) {
                    temp -= 1;
                    wall[i][j][0] = true;
                }
            }
        }
    }

    private static void BFS(int x, int y, int index) {
        Queue<int[]> q = new ArrayDeque<>();
        int count = 1;
        visited[x][y] = true;
        arr[x][y] = index;
        q.add(new int[] {x, y, index});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 4; i++) {
                if (wall[current[0]][current[1]][i]) continue;
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || visited[nx][ny]) continue;
                visited[nx][ny] = true;
                count++;
                arr[nx][ny] = index;
                q.add(new int[] {nx, ny, index});
            }
        }

        rooms.put(index, count);
    }

    private static void setNear(int x, int y, int index) {
        Queue<int[]> q = new ArrayDeque<>();
        visited[x][y] = true;
        q.add(new int[] {x, y});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || visited[nx][ny]) continue;
                if (arr[current[0]][current[1]] != arr[nx][ny]) {
                    near[index].add(arr[nx][ny]);
                    continue;
                }
                visited[nx][ny] = true;
                q.add(new int[] {nx, ny});
            }
        }
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > M-1 || ny < 0 || ny > N-1;
    }
}
```
