```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx =  {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int[][] arr;
    private static boolean[][] visited;
    private static int N, max, min;
    public static void main(String[] args) throws IOException {
        init();

        int answer = binarySearch();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        max = -1;
        min = 201;

        arr = new int[N][N];
        visited = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            for (int j = 0; j < N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                max = Math.max(max, arr[i][j]);
                min = Math.min(min, arr[i][j]);
            }
        }
    }

    private static int binarySearch() {
        int left = 0;
        int right = 200;
        int result = 200;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (valid(mid)) {
                result = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }

        return result;
    }

    private static boolean valid(int diff) {
        for (int i = min; i <= max; i++) {
            int temp = i + diff;

            if (arr[0][0] < i || arr[0][0] > temp || arr[N-1][N-1] < i || arr[N-1][N-1] > temp) continue;

            if (canReach(i, temp)) {
                return true;
            }
        }

        return false;
    }

    private static boolean canReach(int min, int max) {
        Queue<int[]> q = new ArrayDeque<>();
        for (int i = 0; i < N; i++) {
            Arrays.fill(visited[i], false);
        }
        visited[0][0] = true;
        q.add(new int[]{0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == N-1 && current[1] == N-1) {
                return true;
            }

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || arr[nx][ny] > max || arr[nx][ny] < min || visited[nx][ny]) continue;
                visited[nx][ny] = true;
                q.add(new int[] {nx, ny});
            }
        }

        return false;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > N-1;
    }
}
```
