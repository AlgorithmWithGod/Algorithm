```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M,K;
    static char[][] matrix;
    static int[] di = {-1,1,0,0};
    static int[] dj = {0,0,-1,1};
    static int min = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        matrix = new char[N][M];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                matrix[i][j] = line.charAt(j);
            }
        }

        BFS();
        if(min == Integer.MAX_VALUE){
            bw.write("-1");
        }else{
            bw.write(min+"");
        }
        bw.close();
    }
    static void BFS() {
        Queue<int[]> q = new LinkedList<>();
        boolean[][][] visited = new boolean[N][M][K+1];
        q.offer(new int[]{0,0,K,1});//i,j,남은 벽 뚫 개수,현재 거리
        visited[0][0][K] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            if(cur[0] == N-1 && cur[1] == M-1){
                min = Math.min(min, cur[3]);
            }

            for (int k = 0; k < 4; k++) {
                int ni = cur[0] + di[k];
                int nj = cur[1] + dj[k];
                if(ni<0 || ni>=N || nj<0 || nj>=M){
                    continue;
                }
                if(matrix[ni][nj]=='0'){
                    if(!visited[ni][nj][cur[2]]){
                        q.offer(new int[]{ni,nj,cur[2],cur[3]+1});
                        visited[ni][nj][cur[2]] = true;
                    }
                }else if(matrix[ni][nj]=='1'){
                    if(cur[2]>0 && !visited[ni][nj][cur[2]-1]){
                        q.offer(new int[]{ni,nj,cur[2]-1,cur[3]+1});
                        visited[ni][nj][cur[2]-1] = true;
                    }
                }
            }
        }
    }
}

```
