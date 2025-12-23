```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[][] cost = new int[N][N];
        for(int i = 0; i < N; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int j = 0; j < N; j++){
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        boolean[] visited = new boolean[N];
        PriorityQueue<int[]> pq = new PriorityQueue<>(
            (a, b) -> a[1] - b[1]
        );
        pq.offer(new int[]{0, 0});

        long answer = 0;
        int count = 0;
        while(!pq.isEmpty()){
            int[] cur = pq.poll();
            int u = cur[0];
            int c = cur[1];
            if(visited[u])
                continue;

            visited[u] = true;
            answer += c;
            count++;
            if(count == N)
                break;
            for(int v = 0; v < N; v++){
                if(!visited[v]){
                    pq.offer(new int[]{v, cost[u][v]});
                }
            }
        }
        System.out.println(answer);
    }
}

```
