```java
import java.util.*;

class Solution {
    private static int R
    private static int C;
    private static int[][] land;
    private static int[][] idAtPoint;
    private static boolean[][] visited;
    private static int[] dr = {1, -1, 0, 0};
    private static int[] dc = {0, 0, 1, -1};
    private static List<Integer> countAtId;

    public int solution(int[][] lland) {
        land = lland;
        R = land.length;
        C = land[0].length;
        visited = new boolean[R][C];
        idAtPoint = new int[R][C];
        countAtId = new ArrayList<>();
        countAtId.add(0);//0생략
        int id = 1;
        for(int r=0; r<R; r++){
            for(int c=0; c<C; c++){
                if(land[r][c] == 1 && !visited[r][c]){
                    bfs(r, c, id++);
                }
            }
        }

        int answer = 0;
        for(int c=0; c<C; c++){
            int oilAtCol = 0;
            var passedId = new HashSet<Integer>();
            for(int r=0; r<R; r++){
                if(land[r][c] == 0) continue;
                int IdAtP = idAtPoint[r][c];
                if(passedId.contains(IdAtP)) continue;
                passedId.add(IdAtP);
                oilAtCol += countAtId.get(IdAtP);
            }
            answer = Math.max(answer, oilAtCol);
        }
        return answer;
    }

    private void bfs(int sr, int sc, int id){
        var q = new ArrayDeque<int[]>();
        q.add(new int[]{sr, sc});
        visited[sr][sc] = true;
        idAtPoint[sr][sc] = id;

        int temp = 0;
        while(!q.isEmpty()){
            int[] cur = q.poll();
            int r = cur[0]
            int c = cur[1];
            temp++;
            for(int d=0; d<4; d++){
                int nr = r + dr[d];
                int nc = c + dc[d];
                if(nr<0 || nr>=R || nc<0 || nc>=C) continue;
                if(visited[nr][nc]) continue;
                if(land[nr][nc] == 0) continue;
                visited[nr][nc] = true;
                idAtPoint[nr][nc] = id;
                q.add(new int[]{nr, nc});
            }
        }
        countAtId.add(temp);
    }
}

```
