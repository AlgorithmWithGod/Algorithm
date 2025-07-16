```java
import java.util.*;
import java.io.*;

public class Main {
    static int N, K, S, X, Y;
    static int[][] arr;
    static int[] dr = {0, 0, -1, 1};
    static int[] dc = {-1, 1, 0, 0};
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        arr = new int[N+1][N+1];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        Y = Integer.parseInt(st.nextToken());
        br.close();

        // bfs
        bfs();
        System.out.println(arr[X][Y]);

    }
    private static void bfs() {
        PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() { // (바이러스가 퍼진 시간, 바이러스 번호, r, c)
            @Override
            public int compare(int[] o1, int[] o2) {
                if (Integer.compare(o1[0], o2[0]) == 0) {
                    return Integer.compare(o1[1], o2[1]);
                } else {
                    return Integer.compare(o1[0], o2[0]);
                }
            }
        });

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                if (arr[i][j] > 0) {
                    pq.offer(new int[] {0, arr[i][j], i, j});
                }
            }
        }

        while (!pq.isEmpty()) {
            int[] info = pq.poll();
            int curTime = info[0];
            int curVirus = info[1];
            int r = info[2];
            int c = info[3];

            if (curTime == S) continue;
            for (int i = 0; i < 4; i++) {
                int nr = r + dr[i];
                int nc = c + dc[i];
                if (nr < 1 || nr > N || nc < 1 || nc > N) {
                    continue;
                }
                if (arr[nr][nc] > 0) continue;
                arr[nr][nc] = curVirus;
                pq.offer(new int[] {curTime + 1, curVirus, nr, nc});
            }
        }
    }

}
```
