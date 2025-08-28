```java
import java.util.*;
class Solution {
    static int[][] map;
    static int N, M;
    static int[][] dir = new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}};
    public int[] solution(String[] maps) {
        List<Integer> sums = new ArrayList<>();
        N = maps.length;
        M = maps[0].length();
        map = new int[N][M];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                char temp = maps[i].charAt(j);
                if (temp == 'X') map[i][j] = 0;
                else map[i][j] = Integer.parseInt(temp+"");
            }
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] > 0) sums.add(bfs(i, j));
            }
        }
        if (sums.isEmpty()) return new int[]{-1};
        Collections.sort(sums);
        int[] answer = new int[sums.size()];
        for (int i = 0; i < sums.size(); i++) answer[i] = sums.get(i);
        return answer;
    }
    
    static int bfs(int y, int x) {
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[] {y, x});
        int sum = map[y][x];
        map[y][x] = 0;
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            for (int[] d : dir) {
                int ny = cur[0] + d[0];
                int nx = cur[1] + d[1];
                if (ny >= N || ny < 0 || nx >= M || nx < 0 || map[ny][nx] == 0) continue;
                q.offer(new int[] {ny, nx});
                sum += map[ny][nx];
                map[ny][nx] = 0;
            }
        }
        return sum;
    }
}
```
