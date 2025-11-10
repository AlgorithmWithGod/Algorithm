```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        
        boolean[] canStep = new boolean[N + 1];
        Arrays.fill(canStep, true);
        
        for (int i = 0; i < M; i++) {
            int small = Integer.parseInt(br.readLine());
            canStep[small] = false;
        }
        
        int maxSpeed = 200;
        int[][] dist = new int[N + 1][maxSpeed + 1];
        for (int i = 0; i <= N; i++) {
            Arrays.fill(dist[i], Integer.MAX_VALUE);
        }
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[2] - b[2]);
        pq.offer(new int[]{1, 0, 0});
        dist[1][0] = 0;
        
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int pos = cur[0];
            int speed = cur[1];
            int jumps = cur[2];
            
            if (pos == N) {
                System.out.println(jumps);
                return;
            }
            
            if (dist[pos][speed] < jumps) {
                continue;
            }
            
            for (int nextSpeed = Math.max(1, speed - 1); nextSpeed <= speed + 1; nextSpeed++) {
                int nextPos = pos + nextSpeed;
                
                if (nextPos > N || nextPos < 1 || !canStep[nextPos] || nextSpeed > maxSpeed) {
                    continue;
                }
                
                if (dist[nextPos][nextSpeed] > jumps + 1) {
                    dist[nextPos][nextSpeed] = jumps + 1;
                    pq.offer(new int[]{nextPos, nextSpeed, jumps + 1});
                }
            }
        }
        
        System.out.println(-1);
    }
}
```
