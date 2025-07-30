```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static char[][] room;
    static int[] junan = new int[2];
    static int[] friend = new int[2];
    static int[] di = {0,0,-1,1};
    static int[] dj = {-1,1,0,0};
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        room = new char[N+1][M+1];

        st = new StringTokenizer(br.readLine());
        junan[0] = Integer.parseInt(st.nextToken());
        junan[1] = Integer.parseInt(st.nextToken());
        friend[0] = Integer.parseInt(st.nextToken());
        friend[1] = Integer.parseInt(st.nextToken());
        if(junan[0] == friend[0] && junan[1] == friend[1]){
            bw.write("0");
            bw.close();
            return;
        }

        for (int i = 1; i <= N; i++) {
            String line = br.readLine();
            for (int j = 1; j <= M; j++) {
                room[i][j] = line.charAt(j-1);
            }
        }

        bw.write(BFS()+"");
        bw.close();
    }
    static int BFS(){
        ArrayDeque<int[]> q = new ArrayDeque<>();
        boolean[][] visited = new boolean[N+1][M+1];
        q.offer(new int[]{junan[0],junan[1],1});
        visited[junan[0]][junan[1]] = true;

        while(!q.isEmpty()){
            int[] cur = q.poll();
            if(cur[0] == friend[0] && cur[1] == friend[1]){
                return cur[2];
            }
            for (int k = 0; k < 4; k++) {
                int ni = cur[0] + di[k];
                int nj = cur[1] + dj[k];
        
                while (check(ni, nj, visited)){
                    if(room[ni][nj] == '1'){
                        room[ni][nj] = '0';
                        q.offer(new int[]{ni,nj,cur[2]+1});
                        visited[ni][nj] = true;
                        break;
                    }
                    q.push(new int[]{ni,nj,cur[2]});
                    visited[ni][nj] = true;
                    ni += di[k];
                    nj += dj[k];
                }
            }
        }
        return 0;
    }
    static boolean check(int ni,int nj,boolean[][] visited){
        if(ni<=0 || ni>N || nj<=0 || nj>M || visited[ni][nj]){
            return false;
        }else{
            return true;
        }
    }
}
```
