```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
    private static int[] dx = {-1, 1, 0, 0};
    private static int[] dy = {0, 0, -1, 1};
    private static Queue<List<Integer>> queue = new LinkedList<>();

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int M = nextInt(st);
        int N = nextInt(st);
        int map[][] = new int[N][M];

     `   boolean start = false;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = nextInt(st);
                if (map[i][j] == 1) {queue.add(Arrays.asList(i, j, 0)); }
                if (map[i][j] == 0) {
                    start = true;
                }
            }
        }

        if (!start) {
            System.out.println(0);
            return;
        }

        int answer = 0;
        while (!queue.isEmpty()) {
            List<Integer> polled = queue.poll();
            answer = polled.get(2);

            for (int i = 0; i < 4; i++) {
                int nx = polled.get(0) + dx[i];
                int ny = polled.get(1) + dy[i];

                if (nx < 0 || ny < 0 || nx >= N || ny >= M || map[nx][ny] == -1 || map[nx][ny] == 1) {
                    continue;
                }

                map[nx][ny] = 1;
                queue.add(Arrays.asList(nx, ny, answer + 1));
            }
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 0) {
                    System.out.println(-1);
                    return;
                }
            }
        }

        System.out.println(answer);
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
