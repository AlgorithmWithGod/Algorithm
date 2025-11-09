```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {-1, -1, -1, 0, 0, 1, 1, 1};
    private static final int[] dy = {-1, 0, 1, -1, 1, -1, 0, 1};
    private static List<Integer> list;
    private static char[][] map;
    private static boolean[][] visited;
    private static int[][] height;
    private static int[] start;
    private static int N, K;
    public static void main(String[] args) throws IOException {
        init();
        int answer = twoPointer();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        map = new char[N][N];
        height = new int[N][N];
        visited = new boolean[N][N];
        start = new int[2];

        for (int i = 0; i < N; i++) {
            map[i] = br.readLine().toCharArray();
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 'P') {
                    start[0] = i;
                    start[1] = j;
                }
                if (map[i][j] == 'K') K++;
            }
        }

        Set<Integer> set = new TreeSet<>();
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                height[i][j] = Integer.parseInt(st.nextToken());
                set.add(height[i][j]);
            }
        }

        list = new ArrayList<>(set);
    }

    private static int twoPointer() {
        int result = Integer.MAX_VALUE;
        int left = 0;

        for (int right = 0; right < list.size(); right++) {
            while (left <= right) {
                if (valid(list.get(left), list.get(right))) {
                    result = Math.min(result, list.get(right) - list.get(left));
                    left++;
                } else break;
            }
        }

        return result;
    }

    private static boolean valid(int min, int max) {
        if (height[start[0]][start[1]] < min || height[start[0]][start[1]] > max) return false;

        Queue<int[]> q = new ArrayDeque<>();
        for (int i = 0; i < N; i++) Arrays.fill(visited[i], false);
        visited[start[0]][start[1]] = true;
        q.add(new int[]{start[0], start[1]});

        int temp = 0;

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (map[current[0]][current[1]] == 'K') temp++;

            for (int i = 0; i < 8; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || visited[nx][ny] || height[nx][ny] < min || height[nx][ny] > max) continue;

                visited[nx][ny] = true;
                q.add(new int[]{nx, ny});
            }
        }

        return temp == K;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > N-1;
    }
}
```
