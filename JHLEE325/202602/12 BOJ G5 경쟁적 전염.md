```java
import java.io.*;
import java.util.*;

class Virus implements Comparable<Virus> {
    int id, time, r, c;

    public Virus(int id, int time, int r, int c) {
        this.id = id;
        this.time = time;
        this.r = r;
        this.c = c;
    }

    // 바이러스 번호 기준 오름차순 정렬
    @Override
    public int compareTo(Virus o) {
        return this.id - o.id;
    }
}

public class Main {
    static int N, K, S, targetX, targetY;
    static int[][] map;
    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        map = new int[N][N];

        List<Virus> virusList = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (map[i][j] != 0) {
                    virusList.add(new Virus(map[i][j], 0, i, j));
                }
            }
        }

        Collections.sort(virusList);

        Deque<Virus> q = new ArrayDeque<>(virusList);

        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        targetX = Integer.parseInt(st.nextToken());
        targetY = Integer.parseInt(st.nextToken());

        while (!q.isEmpty()) {
            Virus curr = q.poll();

            if (curr.time == S) break;

            for (int i = 0; i < 4; i++) {
                int nr = curr.r + dr[i];
                int nc = curr.c + dc[i];

                if (nr >= 0 && nr < N && nc >= 0 && nc < N) {
                    if (map[nr][nc] == 0) {
                        map[nr][nc] = curr.id;
                        q.add(new Virus(curr.id, curr.time + 1, nr, nc));
                    }
                }
            }
        }

        System.out.println(map[targetX - 1][targetY - 1]);
    }
}
```
