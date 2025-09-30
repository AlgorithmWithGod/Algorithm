```java
import java.io.*;
import java.util.*;

public class boj12869 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();

        int[] hp = new int[3];
        Arrays.fill(hp, 0);

        nextLine();
        for (int i = 0; i < N; i++) hp[i] = nextInt();

        boolean[][][] visited = new boolean[61][61][61];
        Queue<int[]> q = new ArrayDeque<>();
        q.offer(new int[]{hp[0], hp[1], hp[2]});
        visited[hp[0]][hp[1]][hp[2]] = true;

        int[][] dmg = {
                {9,3,1},{9,1,3},
                {3,9,1},{3,1,9},
                {1,9,3},{1,3,9}
        };

        int attacks = 0;
        while (!q.isEmpty()) {
            int sz = q.size();
            for (int s = 0; s < sz; s++) {
                int[] cur = q.poll();
                int a = cur[0], b = cur[1], c = cur[2];
                if (a == 0 && b == 0 && c == 0) {
                    System.out.println(attacks);
                    return;
                }
                for (int[] d : dmg) {
                    int na = Math.max(0, a - d[0]);
                    int nb = Math.max(0, b - d[1]);
                    int nc = Math.max(0, c - d[2]);
                    if (!visited[na][nb][nc]) {
                        visited[na][nb][nc] = true;
                        q.offer(new int[]{na, nb, nc});
                    }
                }
            }
            attacks++;
        }
        System.out.println(attacks);
    }
}
```
