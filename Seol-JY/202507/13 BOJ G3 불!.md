```java
import java.io.*;
import java.util.*;

public class Main {
    static int R, C;
    static char[][] map;
    static int[][] fireTime;
    static int[][] personTime;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
        
        map = new char[R][C];
        fireTime = new int[R][C];
        personTime = new int[R][C];
        
        Deque<int[]> fireQueue = new ArrayDeque<>();
        Deque<int[]> personQueue = new ArrayDeque<>();
        
        for (int i = 0; i < R; i++) {
            Arrays.fill(fireTime[i], -1);
            Arrays.fill(personTime[i], -1);
        }
        
        for (int i = 0; i < R; i++) {
            String line = br.readLine();
            for (int j = 0; j < C; j++) {
                map[i][j] = line.charAt(j);
                if (map[i][j] == 'F') {
                    fireQueue.offer(new int[]{i, j});
                    fireTime[i][j] = 0;
                } else if (map[i][j] == 'J') {
                    personQueue.offer(new int[]{i, j});
                    personTime[i][j] = 0;
                }
            }
        }
        
        while (!fireQueue.isEmpty()) {
            int[] current = fireQueue.poll();
            int x = current[0];
            int y = current[1];
            
            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                
                if (nx < 0 || nx >= R || ny < 0 || ny >= C) continue;
                if (map[nx][ny] == '#' || fireTime[nx][ny] != -1) continue;
                
                fireTime[nx][ny] = fireTime[x][y] + 1;
                fireQueue.offer(new int[]{nx, ny});
            }
        }
        
        while (!personQueue.isEmpty()) {
            int[] current = personQueue.poll();
            int x = current[0];
            int y = current[1];
            
            if (x == 0 || x == R-1 || y == 0 || y == C-1) {
                System.out.println(personTime[x][y] + 1);
                return;
            }
            
            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                
                if (nx < 0 || nx >= R || ny < 0 || ny >= C) continue;
                if (map[nx][ny] == '#' || personTime[nx][ny] != -1) continue;
                
                int nextTime = personTime[x][y] + 1;
                
                if (fireTime[nx][ny] == -1 || fireTime[nx][ny] > nextTime) {
                    personTime[nx][ny] = nextTime;
                    personQueue.offer(new int[]{nx, ny});
                }
            }
        }
        
        System.out.println("IMPOSSIBLE");
    }
}
```
