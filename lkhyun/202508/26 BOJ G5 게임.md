```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    
    static int[][] map = new int[501][501];
    static int[][] dist = new int[501][501];
    static int[] dx = {0, 0, -1, 1};
    static int[] dy = {1, -1, 0, 0};

    public static void main(String[] args) throws IOException {
        for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
        
        int n = Integer.parseInt(br.readLine());
        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            
            for (int x = Math.min(x1, x2); x <= Math.max(x1, x2); x++) {
                for (int y = Math.min(y1, y2); y <= Math.max(y1, y2); y++) {
                    map[x][y] = 1;
                }
            }
        }
        
        int m = Integer.parseInt(br.readLine());
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            
            for (int x = Math.min(x1, x2); x <= Math.max(x1, x2); x++) {
                for (int y = Math.min(y1, y2); y <= Math.max(y1, y2); y++) {
                    map[x][y] = 2;
                }
            }
        }
        
        int result = BFS();
        bw.write(String.valueOf(result));
        bw.close();
    }
    
    private static int BFS() {
        ArrayDeque<int[]> q = new ArrayDeque<>();
        dist[0][0] = 0;
        q.add(new int[]{0, 0});
        
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int x = cur[0], y = cur[1];
            
            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                
                if (nx < 0 || nx > 500 || ny < 0 || ny > 500 || map[nx][ny] == 2) continue;
                
                int newDist = dist[x][y] + map[nx][ny];
                if (newDist < dist[nx][ny]) {
                    dist[nx][ny] = newDist;
                    if (map[nx][ny] == 0) q.addFirst(new int[]{nx, ny});
                    else q.addLast(new int[]{nx, ny});
                }
            }
        }
        
        return dist[500][500] == Integer.MAX_VALUE ? -1 : dist[500][500];
    }
}
```
