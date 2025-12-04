```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int h, w;
    private static char[][] map;
    private static int[][][] doors;
    private static int[][] prisoners;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            int answer = 10001;

            init();
            for (int i = 0; i < 3; i++) {
                BFS(i);
            }

            for (int i = 1; i <= h; i++) {
                for (int j = 1; j <= w; j++) {
                    if (map[i][j] == '.' || map[i][j] == '$') {
                        int sum = doors[0][i][j] + doors[1][i][j] + doors[2][i][j];
                        answer = Math.min(answer, sum);
                    } else if (map[i][j] == '#') {
                        int sum = doors[0][i][j] + doors[1][i][j] + doors[2][i][j] - 2;
                        answer = Math.min(answer, sum);
                    }
                }
            }

            bw.write(answer + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        h = Integer.parseInt(st.nextToken());
        w = Integer.parseInt(st.nextToken());

        map = new char[h+2][w+2];
        doors = new int[3][h+2][w+2];
        prisoners = new int[2][2];
        int index = 0;

        for (int i = 1; i <= h; i++) {
            char[] input = br.readLine().toCharArray();

            for (int j = 1; j <= w; j++) {
                map[i][j] = input[j-1];
                if (map[i][j] == '$') {
                    prisoners[index][0] = i;
                    prisoners[index++][1] = j;
                }
            }
        }

        for (int i = 0; i <= h+1; i++) {
            map[i][0] = '.';
            map[i][w+1] = '.';
        }

        for (int i = 0; i <= w+1; i++) {
            map[0][i] = '.';
            map[h+1][i] = '.';
        }
    }

    private static void BFS(int index) {
        Queue<int[]> q = new ArrayDeque<>();

        for (int i = 0; i <= h+1; i++) {
            Arrays.fill(doors[index][i], 10001);
        }

        if (index == 2) {
            doors[index][0][0] = 0;
            q.add (new int[] {0, 0});
        }
        else {
            doors[index][prisoners[index][0]][prisoners[index][1]] = 0;
            q.add(new int[] {prisoners[index][0], prisoners[index][1]});
        }

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] == '*') continue;
                if (map[nx][ny] == '#' && doors[index][current[0]][current[1]]+1 < doors[index][nx][ny]) {
                    doors[index][nx][ny] = doors[index][current[0]][current[1]]+1;
                    q.add(new int[] {nx, ny});
                } else if ((map[nx][ny] == '.' || map[nx][ny] == '$') && doors[index][current[0]][current[1]] < doors[index][nx][ny]) {
                    doors[index][nx][ny] = doors[index][current[0]][current[1]];
                    q.add(new int[] {nx, ny});
                }
            }
        }
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > h+1 || ny < 0 || ny > w+1;
    }
}
```
