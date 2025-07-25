```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static char[][] map;
    static List<int[]> lands;
    static int[] di = {0,0,-1,1};
    static int[] dj = {-1,1,0,0};
    static int ans = 0;
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        map = new char[N][M];
        lands = new LinkedList<>();

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                map[i][j] = line.charAt(j);
                if(map[i][j] == 'L'){
                    lands.add(new int[]{i,j});
                }
            }
        }
        

        for (int[] cur : lands) {
            BFS(cur[0],cur[1]);
        }
        bw.write(ans+"");
        bw.close();
    }
    static void BFS(int starti, int startj){
        ArrayDeque<int[]> q = new ArrayDeque<>();
        boolean[][] visited = new boolean[N][M];
        q.add(new int[]{starti,startj,0});
        visited[starti][startj] = true;

        while(!q.isEmpty()){
            int[] cur = q.poll();
            ans = Math.max(ans,cur[2]);
            
            for (int k = 0; k < 4; k++) {
                int ni = cur[0] + di[k];
                int nj = cur[1] + dj[k];

                if(ni<0 || ni>=N || nj<0 || nj>=M || visited[ni][nj]) continue;

                if(map[ni][nj] == 'L'){
                    q.add(new int[]{ni,nj,cur[2]+1});
                    visited[ni][nj] = true;
                }
            }
        }
    }
}
```
