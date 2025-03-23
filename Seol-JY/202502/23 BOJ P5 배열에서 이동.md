```java
import java.io.*;
import java.util.*;

public class Main {
    static final int[] dr = {-1, 1, 0, 0};
    static final int[] dc = {0, 0, 1, -1};
    static int N;
    static int[][] map;
    static boolean[][] visited;
    static int minValue, maxValue;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        map = new int[N][N];
        visited = new boolean[N][N];

        minValue = 201;
        maxValue = 0;

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                minValue = Math.min(minValue, map[i][j]);
                maxValue = Math.max(maxValue, map[i][j]);
            }
        }

        System.out.println(solve());
    }

    private static int solve() {
        int left = 0;
        int right = maxValue - minValue;
        int result = right;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (isPossible(mid)) {
                result = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return result;
    }

    private static boolean isPossible(int diff) {
        for (int min = minValue; min <= maxValue - diff; min++) {
            int max = min + diff;
            if (map[0][0] < min || map[0][0] > max) continue;

            for (int i = 0; i < N; i++) {
                Arrays.fill(visited[i], false);
            }

            if (bfs(min, max)) return true;
        }
        return false;
    }

    private static boolean bfs(int min, int max) {
        ArrayDeque<Position> deque = new ArrayDeque<>();
        deque.offer(new Position(0, 0));
        visited[0][0] = true;

        while (!deque.isEmpty()) {
            Position target = deque.poll();

            if (target.r == N-1 && target.c == N-1) return true;

            for (int i = 0; i < 4; i++) {
                int nr = target.r + dr[i];
                int nc = target.c + dc[i];

                if (nr < 0 || nc < 0 || nr >= N || nc >= N || visited[nr][nc]) continue;
                if (map[nr][nc] < min || map[nr][nc] > max) continue;

                visited[nr][nc] = true;
                deque.offer(new Position(nr, nc));
            }
        }

        return false;
    }

    static class Position {
        int r;
        int c;

        public Position(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }
}
```
