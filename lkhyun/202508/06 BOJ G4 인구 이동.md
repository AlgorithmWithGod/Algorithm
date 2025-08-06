```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,L,R;
    static int[][] A;
    static int[] di = {0,0,-1,1};
    static int[] dj = {-1,1,0,0};

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());

        A = new int[N][N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                A[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        int ans = 0;
        while(BFS()){
            ans++;
        }
        bw.write(ans+"");
        bw.close();
    }
    static boolean BFS(){
        boolean check = false;
        boolean[][] visited = new boolean[N][N];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if(!visited[i][j]){
                    ArrayDeque<int[]> q = new ArrayDeque<>();
                    q.offer(new int[]{i,j});
                    visited[i][j] = true;

                    int sum = 0;
                    List<int[]> saveList = new ArrayList<>();
                    while(!q.isEmpty()){
                        int[] cur = q.poll();
                        saveList.add(cur);

                        sum += A[cur[0]][cur[1]];

                        for (int k = 0; k < 4; k++) {
                            int ni = cur[0] + di[k];
                            int nj = cur[1] + dj[k];

                            if(ni<0 || ni>=N || nj<0 || nj>=N || visited[ni][nj]) continue;

                            int cond = Math.abs(A[ni][nj]-A[cur[0]][cur[1]]);
                            if(cond >= L && cond <= R){
                                q.offer(new int[]{ni,nj});
                                visited[ni][nj] = true;
                            }
                        }
                    }
                    if(saveList.size() > 1){
                        check = true;
                        sum = sum/saveList.size();
                        for (int[] s : saveList) {
                            A[s[0]][s[1]] = sum;
                        }
                    }
                }
            }
        }
        return check;
    }
}
```
