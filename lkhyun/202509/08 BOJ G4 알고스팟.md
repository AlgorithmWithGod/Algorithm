```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static int[] di = {-1,1,0,0};
    static int[] dj = {0,0,-1,1};
    static int[][] matrix;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());

        matrix = new int[N][M];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                matrix[i][j] = Character.getNumericValue(line.charAt(j));
            }
        }
        bw.write(BFS()+"");
        bw.close();
    }
    public static int BFS(){
        ArrayDeque<int[]> deq = new ArrayDeque<>();
        boolean[][] visited = new boolean[N][M];
        deq.offer(new int[]{0,0,0});
        visited[0][0] = true;

        while(!deq.isEmpty()){
            int[] cur = deq.poll();
            
            if(cur[0] == N-1 && cur[1] == M-1) return cur[2];

            for (int i = 0; i < 4; i++) {
                int ni = cur[0] + di[i];
                int nj = cur[1] + dj[i];

                if(ni<0 || ni>=N || nj<0 || nj>=M || visited[ni][nj]) continue;

                if(matrix[ni][nj] == 0){
                    deq.offerFirst(new int[]{ni,nj,cur[2]});
                    visited[ni][nj] = true;
                }else{
                    deq.offer(new int[]{ni,nj,cur[2]+1});
                    visited[ni][nj] = true;
                }
            }
        }
        return 0;
    }
}
```
