```java
import java.util.*;

class Solution {
    static class Point{
        int r;
        int c;
        Point(int r, int c){
            this.r = r;
            this.c = c;
        }
        Point translate(int dr, int dc){
            return new Point(r+dr, c+dc);
        }
    }
    private static int[][] Drdcs = {
        {0, 1},
        {1, 0},
        {0, -1},
        {-1, 0}
    };
    private static int R;
    private static int C;
    private static int[][] Map;
    private static HashMap<Integer, LinkedList<Point>> PointsOfId;
    public int solution(String[] storages, String[] requests) {
        C = storages[0].length();
        R = storages.length;
        int answer = R*C;
        Map = new int[R+2][C+2];
        PointsOfId = new HashMap<Integer, LinkedList<Point>>();
        for(int r = 0; r < R; r++){
            String storage = storages[r];
            for(int c = 0; c< C; c++){
                char cc = storage.charAt(c);
                int id = cc - 'A' + 1;
                var points = PointsOfId.get(id);
                if(points == null){
                    points = new LinkedList<Point>();
                    PointsOfId.put(id, points);
                }
                points.add(new Point(r+1, c+1));
                Map[r+1][c+1] = id;
            }
        }
        
        Integer preTarget = null;
        for(String request: requests){
            int target = request.charAt(0) - 'A'+1;
            if(request.length() != 1){
                // for(Point p: PointsOfId.get(target)){ 런타임 에러!!!!
                //     Map[p.r][p.c] = 0;
                //     answer--;
                // }
                for(Point p: PointsOfId.getOrDefault(target, new LinkedList<Point>())){
                    Map[p.r][p.c] = 0;
                    answer--;
                }
                continue;
            }
            var visited = new boolean[R+2][C+2];
            
            var startP = new Point(0, 0);
            visit(visited, startP);
            var q = new ArrayDeque<Point>();
            q.offer(startP);
            while(!q.isEmpty()){
                Point p = q.poll();
                for(int[] drdc: Drdcs){
                    var nextP = p.translate(drdc[0], drdc[1]);
                    if(BC(nextP)) continue;
                    if(isVisit(visited, nextP)) continue;
                    if(getIdAt(nextP) == target){
                        Map[nextP.r][nextP.c] = 0;
                        visit(visited, nextP);
                    }else if(getIdAt(nextP) == 0){
                        visit(visited, nextP);
                        q.offer(nextP);
                    }
                }
            }
            // p(Map);
            // System.out.println();
        }
        
        int a2 = 0;
        for(int r = 0; r<R+2; r++)
            for(int c = 0; c<C+2; c++)
                if(Map[r][c]!=0) a2++;
        return a2;
    }
    
    private void p(int[][] map){
        for(int[] m: map){
            System.out.println(Arrays.toString(m));
        }
    }
    private int getIdAt(Point p){
        return Map[p.r][p.c];
    }
    private void visit(boolean[][] v, Point p ){
        v[p.r][p.c] = true;
    }
    private boolean isVisit(boolean[][] v, Point p ){
        return v[p.r][p.c];
    }
    private boolean BC(Point p){
        int r = p.r;
        int c = p.c;
        return r < 0 || r>= R+2 || c < 0 || c>=C+2;
    }
}
```
