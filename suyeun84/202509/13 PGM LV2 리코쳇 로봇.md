```java
import java.util.*;
class Solution {
    static int[][] dir = new int[][]{{1,0}, {-1,0}, {0,1}, {0,-1}};
    static int answer = -1;
    static Point start, target;
    static int N, M;
    static char[][] map;
    static int[][] visited;
    
    public int solution(String[] board) {
        N = board.length;
        M = board[0].length();
        map = new char[N][M];
        visited = new int[N][M];
        for (int i = 0; i < N; i++) {
            map[i] = board[i].toCharArray();
            Arrays.fill(visited[i], Integer.MAX_VALUE);
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 'R') start = new Point(i, j, 0);
                else if (map[i][j] == 'G') target = new Point(i, j, 0);
            }
        }
        
        bfs();
        
        return answer;
    }
    
    private void bfs() {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(start.y, start.x, start.cnt));
        visited[start.y][start.x] = 0;
        while (!q.isEmpty()) {
            Point curr = q.poll();
            if (curr.y == target.y && curr.x == target.x) {
                answer = curr.cnt;
                return;
            }
            
            for (int[] d : dir) {
                int ny = curr.y, nx = curr.x;
                while (true) {
                    ny += d[0];
                    nx += d[1];
                    if (ny < 0 || ny >= N || nx < 0 || nx >= M || map[ny][nx] == 'D') {
                        ny -= d[0];
                        nx -= d[1];
                        if (visited[ny][nx] <= curr.cnt+1) break;
                        q.add(new Point(ny, nx, curr.cnt+1));
                        visited[ny][nx] = curr.cnt+1;
                    }
                }
            }
        }
        
    }
    
    class Point {
        int y, x, cnt;
        public Point(int y, int x, int cnt) {
            this.y = y;
            this.x = x;
            this.cnt = cnt;
        }
    }
}
```
