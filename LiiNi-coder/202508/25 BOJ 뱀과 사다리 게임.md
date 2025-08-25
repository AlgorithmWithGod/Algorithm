```java
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br;
    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        String[] temp = br.readLine().split(" ");
        int N = Integer.parseInt(temp[0]);
        int M = Integer.parseInt(temp[1]);

        Map<Integer, Integer> move = new HashMap<>();
        for (int i = 0; i < N; i++) {
            temp = br.readLine().split(" ");
            move.put(Integer.parseInt(temp[0]), Integer.parseInt(temp[1]));
        }
        for (int i = 0; i < M; i++) {
            temp = br.readLine().split(" ");
            move.put(Integer.parseInt(temp[0]), Integer.parseInt(temp[1]));
        }
        boolean[] visited = new boolean[101];
        Queue<int[]> q = new ArrayDeque<>();
        q.add(new int[]{1, 0}); //QElement: {현재칸, 주사위횟수}
        visited[1] = true;
        while (!q.isEmpty()) {
            //
            int[] cur = q.poll();
            int now = cur[0];
            int count = cur[1];
            if (now == 100) {
                System.out.println(count);
                return;
            }

            for (int d = 1; d <= 6; d++) {
                int np = now + d;
                if (np > 100) continue;
                if (move.containsKey(np))
                    np = move.get(np);
                if (!visited[np]) {
                    visited[np] = true;
                    q.add(new int[]{np, count + 1});
                }
            }
        }
    }
}
```
