```java
import java.util.*;
class Solution {
    static int[][] dir = new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}};
    static int N, M;
    static char[][] stor;
    public int solution(String[] storage, String[] requests) {
        int answer = 0;
        N = storage.length;
        M = storage[0].length();
        stor = new char[N][M];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                stor[i][j] = storage[i].charAt(j);
            }
        }
        for (String request : requests) {
            int type = request.length();
            if (type == 1) {
                ArrayList<int[]> arr = new ArrayList<>();
                for (int i = 0; i < N; i++) {
                    for (int j = 0; j < M; j++) {
                        if (stor[i][j] != request.charAt(0)) continue;
                        if (i == 0 || i == N-1 || j == 0 || j == M-1 || check(i, j)) arr.add(new int[]{i, j});
                    }
                }
                for (int[] a : arr) stor[a[0]][a[1]] = '0';
            } else if (type == 2) {
                for (int i = 0; i < N; i++) {
                    for (int j = 0; j < M; j++) {
                        if (stor[i][j] == request.charAt(0)) stor[i][j] = '0';
                    }
                }
            }
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (stor[i][j] != '0') answer++;
            }
        }
        return answer;
    }
    
    static boolean check(int i, int j) {
        boolean[][] visited = new boolean[N][M];
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[] {i, j});
        visited[i][j] = true;
        while (!q.isEmpty()) {
            int[] curr = q.poll();
            for (int[] d : dir) {
                int ny = curr[0] + d[0];
                int nx = curr[1] + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M || visited[ny][nx] || stor[ny][nx] != '0') continue;
                if (ny == 0 || ny == N-1 || nx == 0 || nx == M-1) return true;
                q.add(new int[] {ny, nx});
                visited[ny][nx] = true;
            }
        }
        return false;
    }
}
```
