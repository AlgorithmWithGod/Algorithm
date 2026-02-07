```java
import java.io.*;
import java.util.*;

public class Main {
    
    static int N, M;
    static int[][] map;
    static int[] dx = {0, 0, -1, -1, -1, 0, 1, 1, 1}; // 1~8 방향
    static int[] dy = {0, -1, -1, 0, 1, 1, 1, 0, -1};
    static boolean[][] wasCloud;
    static List<int[]> clouds = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        map = new int[N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        clouds.add(new int[]{N - 1, 0});
        clouds.add(new int[]{N - 1, 1});
        clouds.add(new int[]{N - 2, 0});
        clouds.add(new int[]{N - 2, 1});

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int d = Integer.parseInt(st.nextToken());
            int s = Integer.parseInt(st.nextToken());
            solve(d, s);
        }

        int sum = 0;
        for (int[] row : map) {
            for (int val : row) sum += val;
        }
        System.out.println(sum);
    }

    static void solve(int d, int s) {
        wasCloud = new boolean[N][N];

        for (int[] cloud : clouds) {
            int nx = (cloud[0] + dx[d] * (s % N) + N) % N;
            int ny = (cloud[1] + dy[d] * (s % N) + N) % N;

            map[nx][ny]++;
            wasCloud[nx][ny] = true;
            cloud[0] = nx;
            cloud[1] = ny;
        }

        for (int[] cloud : clouds) {
            int cx = cloud[0];
            int cy = cloud[1];
            int count = 0;
            for (int i = 2; i <= 8; i += 2) {
                int nx = cx + dx[i];
                int ny = cy + dy[i];
                if (nx >= 0 && nx < N && ny >= 0 && ny < N && map[nx][ny] > 0) {
                    count++;
                }
            }
            map[cx][cy] += count;
        }

        List<int[]> nextClouds = new ArrayList<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] >= 2 && !wasCloud[i][j]) {
                    map[i][j] -= 2;
                    nextClouds.add(new int[]{i, j});
                }
            }
        }
        clouds = nextClouds;
    }
}
```
