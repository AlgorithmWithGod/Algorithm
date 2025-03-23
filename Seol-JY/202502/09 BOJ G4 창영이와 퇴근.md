```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int N = Integer.parseInt(br.readLine());
        int[][] grid = new int[N][N];
        
        // 입력
        for(int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int j = 0; j < N; j++) {
                grid[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        // 다익스트라를 위한 초기화
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[2] - b[2]); // [x, y, maxDiff]
        boolean[][] visited = new boolean[N][N];
        int[][] dist = new int[N][N];
        for(int i = 0; i < N; i++) {
            Arrays.fill(dist[i], Integer.MAX_VALUE);
        }
        
        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};
        
        dist[0][0] = 0;
        pq.offer(new int[]{0, 0, 0});
        
        while(!pq.isEmpty()) {
            int[] current = pq.poll();
            int x = current[0];
            int y = current[1];
            
            if(visited[x][y]) continue;
            visited[x][y] = true;
            
            for(int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                
                if(nx < 0 || nx >= N || ny < 0 || ny >= N || visited[nx][ny]) continue;
                
                int diff = Math.abs(grid[nx][ny] - grid[x][y]);
                int maxDiff = Math.max(dist[x][y], diff);
                
                if(dist[nx][ny] > maxDiff) {
                    dist[nx][ny] = maxDiff;
                    pq.offer(new int[]{nx, ny, maxDiff});
                }
            }
        }
        
        System.out.println(dist[N-1][N-1]);
    }
}
```
