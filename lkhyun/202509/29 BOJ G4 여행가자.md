```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,M;
    static int[][] cities;
    static int[] travel;
    static Set<Integer> connected = new HashSet<>();

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());
        cities = new int[N+1][N+1];
        travel = new int[M];
        
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                cities[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            travel[i] = Integer.parseInt(st.nextToken());
        }

        BFS(travel[0]);
        for (int i = 0; i < M; i++) {
            if(!connected.contains(travel[i])){
                bw.write("NO");
                bw.close();
                return;
            }
        }
        bw.write("YES");
        bw.close();
    }
    public static void BFS(int start){
        ArrayDeque<Integer> q = new ArrayDeque<>();
        boolean[] visited = new boolean[N+1];
        q.offer(start);
        visited[start] = true;

        while(!q.isEmpty()){
            int cur = q.poll();
            connected.add(cur);
            
            for (int i=1;i<=N;i++) {
                if(cities[cur][i] == 0 || visited[i]) continue;
                q.offer(i);
                visited[i] = true;
            }
        }
    }
}
```
