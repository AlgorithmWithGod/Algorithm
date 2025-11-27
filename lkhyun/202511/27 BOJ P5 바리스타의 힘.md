```java
import java.util.*;
import java.io.*;

public class Main{
    static class State{
        int i,j,cnt;
        State(int i,int j, int cnt){
            this.i = i;
            this.j = j;
            this.cnt = cnt;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,M;
    static int[][] map;
    static int[] di = {-1, 1, 0, 0};
    static int[] dj = {0, 0, -1, 1};
    static int ans = Integer.MAX_VALUE;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N+1][M+1];

        for(int i = 1; i<=N; i++){
            String line = br.readLine();
            for(int j = 1; j<=M; j++){
                map[i][j] = Character.getNumericValue(line.charAt(j-1));
            }
        }

        BFS();
        bw.write((ans == Integer.MAX_VALUE ? -1 : ans) + "");
        bw.close();
    }
    
    public static void BFS(){
        int[][][] dist = new int[N+1][M+1][2];
        for(int i = 0; i <= N; i++){
            for(int j = 0; j <= M; j++){
                dist[i][j][0] = -1;
                dist[i][j][1] = -1;
            }
        }
        
        int[] leftmostInRow = new int[N+1];
        Arrays.fill(leftmostInRow, -1);
        
        int[] topmostInCol = new int[M+1];
        Arrays.fill(topmostInCol, -1);
        
        ArrayDeque<State> q = new ArrayDeque<>();
        
        //출발지에서 BFS
        q.offer(new State(1, 1, 0));
        dist[1][1][0] = 0;
        leftmostInRow[1] = 1;
        topmostInCol[1] = 1;
        
        while(!q.isEmpty()){
            State cur = q.poll();
            
            for(int d = 0; d < 4; d++){
                int ni = cur.i + di[d];
                int nj = cur.j + dj[d];
                
                if(OOB(ni, nj)) continue;
                if(map[ni][nj] == 1) continue;
                if(dist[ni][nj][0] != -1) continue;
                
                dist[ni][nj][0] = cur.cnt + 1;
                q.offer(new State(ni, nj, cur.cnt + 1));
                
                //현재 행에서 가장 왼쪽 열 저장
                if(leftmostInRow[ni] == -1 || leftmostInRow[ni] > nj){
                    leftmostInRow[ni] = nj;
                }
                //현재 열에서 가장 위쪽 열 저장
                if(topmostInCol[nj] == -1 || topmostInCol[nj] > ni){
                    topmostInCol[nj] = ni;
                }
            }
        }
        
        //도착지에서 BFS
        q.offer(new State(N, M, 0));
        dist[N][M][1] = 0;
        
        while(!q.isEmpty()){
            State cur = q.poll();
            
            for(int d = 0; d < 4; d++){
                int ni = cur.i + di[d];
                int nj = cur.j + dj[d];
                
                if(OOB(ni, nj)) continue;
                if(map[ni][nj] == 1) continue;
                if(dist[ni][nj][1] != -1) continue;
                
                dist[ni][nj][1] = cur.cnt + 1;
                q.offer(new State(ni, nj, cur.cnt + 1));
            }
        }
        //일단 벽 안뚫고도 만날 수 있으면 값 저장. 앞으로 벽뚫어서 최적될 수도 있음.
        if(dist[N][M][0] != -1){
            ans = dist[N][M][0];
        }
        
        //행 단위로 쭉 보면서 가장 왼쪽 부분에서 오른쪽으로 기술 사용
        for(int i = 1; i <= N; i++){
            if(leftmostInRow[i] == -1) continue; //애초에 못가는 부분임.
            int j = leftmostInRow[i];
            
            int nj = j + 1;
            int distance = 0;
            while(!OOB(i, nj)){
                distance++;
                //도착지에서 온 지점과 바로 만나는 경우
                if(dist[i][nj][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + dist[i][nj][1]);
                }
                //오른쪽으로 기술을 사용해서 아래쪽으로 길이 뚤리는 경우
                if(!OOB(i+1, nj) && dist[i+1][nj][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + 1 + dist[i+1][nj][1]);
                }
                //오른쪽으로 기술을 사용해서 위쪽으로 길이 뚤리는 경우
                if(!OOB(i-1, nj) && dist[i-1][nj][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + 1 + dist[i-1][nj][1]);
                }
                nj++;
            }
        }
        
        //모든 열에 대해서 가장 위쪽 값에서 기술 사용
        for(int j = 1; j <= M; j++){
            if(topmostInCol[j] == -1) continue;
            int i = topmostInCol[j];
            
            int ni = i + 1;
            int distance = 0;
            while(!OOB(ni, j)){
                distance++;
                //바로 만나는 경우
                if(dist[ni][j][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + dist[ni][j][1]);
                }
                //아래로 기술 사용해서 오른쪽으로 길이 뚤리는 경우
                if(!OOB(ni, j+1) && dist[ni][j+1][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + 1 + dist[ni][j+1][1]);
                }
                //아래로 기술 사용해서 왼쪽으로 길이 뚫리는 경우
                if(!OOB(ni, j-1) && dist[ni][j-1][1] != -1){
                    ans = Math.min(ans, dist[i][j][0] + distance + 1 + dist[ni][j-1][1]);
                }
                ni++;
            }
        }
    }
    
    public static boolean OOB(int i, int j){
        return (i<1 || i>N || j<1 || j>M);
    }
}
```
