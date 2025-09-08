```java
import java.util.*;
class Solution {
    public int solution(int[][] maps) {
        
        return bfs(maps);
    }
    public int bfs(int[][] maps) {
        int n = maps.length;
        int m = maps[0].length;
        int[][] d = new int[][]{{1,0}, {-1,0}, {0,1}, {0,-1}};
        int[][] visited = new int[n][m];
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{0, 0, 1});
        visited[0][0] = 1;
        while (!q.isEmpty()) {
            int[] curr = q.poll();
            for (int[] move : d) {
                int ny = curr[0] + move[0];
                int nx = curr[1] + move[1];
                if (0 > ny || ny >= n || 0 > nx || nx >= m || maps[ny][nx] == 0 || visited[ny][nx] != 0) {
                    continue;
                }
                visited[ny][nx] = curr[2] + 1;
                q.add(new int[]{ny, nx, curr[2]+1});
                if (ny == n-1 && nx == m-1) {
                    return visited[ny][nx];
                }
            }
        }
        return -1;
    }
}
```
