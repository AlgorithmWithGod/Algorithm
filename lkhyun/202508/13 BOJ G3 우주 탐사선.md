```java
import java.io.*;
import java.util.*;

public class Main {
    static int ans;
    static int N,K;
    static int[][] dist;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        dist = new int[N][N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                dist[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    
        for (int k = 0; k < N; k++) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }

        ans = Integer.MAX_VALUE;
        boolean[] visited = new boolean[N];
        visited[K] = true;
        find(visited,1,0,K);
        
        bw.write(ans + "");
        bw.close();
    }

    static void find(boolean[] visited, int depth, int sum, int prev){
        if(depth == N){
            ans = Math.min(ans,sum);
            return;
        }
        if(sum >= ans) return;
        for (int i = 0; i < N; i++) {
            if(!visited[i]){
                visited[i] = true;
                find(visited, depth+1,sum+dist[prev][i], i);
                visited[i] = false;
            }
        }
    }
    
}
```
