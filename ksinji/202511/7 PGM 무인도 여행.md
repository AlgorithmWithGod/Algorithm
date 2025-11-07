```java
import java.util.*;

class Solution {
    static final int[] dx = {1,-1,0,0};
    static final int[] dy = {0,0,1,-1};

    public int[] solution(String[] maps) {
        int n = maps.length;
        int m = maps[0].length();
        boolean[][] visited = new boolean[n][m];
        List<Integer> ans = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (maps[i].charAt(j) == 'X' || visited[i][j]) continue;

                int sum = 0;
                ArrayDeque<int[]> q = new ArrayDeque<>();
                q.offer(new int[]{i, j});
                visited[i][j] = true;

                while (!q.isEmpty()) {
                    int[] cur = q.poll();
                    int y = cur[0], x = cur[1];
                    sum += maps[y].charAt(x) - '0';

                    for (int d = 0; d < 4; d++) {
                        int ny = y + dy[d], nx = x + dx[d];
                        if (ny < 0 || nx < 0 || ny >= n || nx >= m) continue;
                        if (visited[ny][nx] || maps[ny].charAt(nx) == 'X') continue;
                        visited[ny][nx] = true;
                        q.offer(new int[]{ny, nx});
                    }
                }
                ans.add(sum);
            }
        }

        if (ans.isEmpty()) return new int[]{-1};
        Collections.sort(ans);
        return ans.stream().mapToInt(Integer::intValue).toArray();
    }
}

```
