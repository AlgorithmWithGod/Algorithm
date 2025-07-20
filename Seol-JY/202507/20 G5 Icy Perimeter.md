```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static char[][] map;
    static boolean[][] vis;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    static int area, perimeter;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        
        map = new char[n][n];
        vis = new boolean[n][n];
        
        for (int i = 0; i < n; i++) {
            map[i] = br.readLine().toCharArray();
        }
        
        int maxArea = 0;
        int minPeri = Integer.MAX_VALUE;
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (map[i][j] != '#' || vis[i][j]) continue;
                
                area = 0;
                perimeter = 0;
                dfs(i, j);
                
                if (area > maxArea || (area == maxArea && perimeter < minPeri)) {
                    maxArea = area;
                    minPeri = perimeter;
                }
            }
        }
        
        System.out.println(maxArea + " " + minPeri);
    }
    
    static void dfs(int x, int y) {
        vis[x][y] = true;
        area++;
        
        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];
            
            if (nx < 0 || nx >= n || ny < 0 || ny >= n || map[nx][ny] == '.') {
                perimeter++;
                continue;
            }
            
            if (map[nx][ny] == '#' && !vis[nx][ny]) {
                dfs(nx, ny);
            }
        }
    }
}
```
