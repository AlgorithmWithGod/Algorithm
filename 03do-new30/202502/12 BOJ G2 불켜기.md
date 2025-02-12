```java
import java.io.*;
import java.util.*;

public Main {
    static class Point {
        int r;
        int c;
        public Point(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }

    static int[] dr = {0, 0, -1, 1};
    static int[] dc = {-1, 1, 0, 0};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        // 스위치 정보 저장
        List<Point>[][] buttons = new ArrayList[N+1][N+1];
        for (int i = 1; i < N+1; i++) {
            for (int j = 1; j < N+1; j++) {
                buttons[i][j] = new ArrayList<>();
            }
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int r = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int nr = Integer.parseInt(st.nextToken());
            int nc = Integer.parseInt(st.nextToken());
            buttons[r][c].add(new Point(nr, nc));
        }

        // light[i][j] = (i, j) 방에 불이 켜짐
        boolean[][] light = new boolean[N+1][N+1];
        light[1][1] = true;
        // visited[i][j] = (i, j)방에 도착함
        boolean[][] visited = new boolean[N+1][N+1];
        visited[1][1] = true;

        Queue<Point> q = new ArrayDeque<>();
        q.offer(new Point(1, 1));

        // (i, j)로 움직일 수 있는 조건은
        // light[i][j]가 참이면서 visited[i][j]가 참인 지점!
        while (!q.isEmpty()) {
            Point p = q.poll();

            // p 지점에서 켤 수 있는 스위치를 모두 켠다
            for (Point np : buttons[p.r][p.c]) {

                if (light[np.r][np.c]) { continue; }

                light[np.r][np.c] = true; // 스위치 켬

                // 이전에 방문한 적이 있는데 이번에 불이 켜졌다면 도달 가능한 지점!
                if (visited[np.r][np.c]) {
                    q.offer(np); // 큐에 삽입
                }
            }

            for (int i = 0; i < 4; i++) {

                int nr = p.r + dr[i];
                int nc = p.c + dc[i];

                if (1 <= nr && nr < N+1 && 1 <= nc && nc < N+1) {
                    if (visited[nr][nc]) { continue; }

                    // 방문 표시
                    visited[nr][nc] = true;
                    // 만약 불이 켜져 있는 곳이라면 큐에 삽입!
                    if (light[nr][nc]) {
                        q.offer(new Point(nr, nc));
                    }
                }
            }
        }

        int answer = 0;
        for (int i = 1; i < N+1; i++) {
            for (int j = 1; j < N+1; j++) {
                if (light[i][j]) { answer++; }
            }
        }

        bw.write(answer + "\n");


        br.close();
        bw.flush();
        bw.close();
    }
}
```
