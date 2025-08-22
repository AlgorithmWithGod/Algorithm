```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static class Edge{
        int to;
        int cnt;
        int cost;

        Edge(int to, int cnt, int cost){
            this.to = to;
            this.cnt = cnt;
            this.cost = cost;
        }
    }
    static int N,M,K;
    static int S,D;
    static List<Edge>[] adjLists;
    static int[][] dist;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        adjLists = new List[N+1];
        dist = new int[N+1][N+1];
        
        for (int i = 1; i <= N; i++) {
            adjLists[i] = new ArrayList<>();
            Arrays.fill(dist[i], Integer.MAX_VALUE);
        }

        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            adjLists[from].add(new Edge(to, 0, cost));
            adjLists[to].add(new Edge(from, 0, cost));
        }

        dijkstra(S);
        
        int optIdx = 0;
        int ans = Integer.MAX_VALUE;
        for (int i = 1; i <= N; i++) {
            if(dist[D][i] < ans){
                ans = dist[D][i];
                optIdx = i;
            }
        }
        StringBuilder sb = new StringBuilder();
        sb.append(ans).append("\n");

        int tax = 0;
        for (int i = 0; i < K; i++) {
            tax += Integer.parseInt(br.readLine());
            ans = Integer.MAX_VALUE;
            for (int j = 1; j <= N; j++) {
                if(dist[D][j] == Integer.MAX_VALUE) continue;
                int cur = dist[D][j] + (tax*j);
                if(cur < ans){
                    ans = cur;
                    optIdx = j;
                }
            }
            sb.append(ans).append("\n");
        }
        bw.write(sb.toString());
        bw.close();
    }
    
    public static void dijkstra(int start){
        PriorityQueue<Edge> pq = new PriorityQueue<>((a,b) -> a.cost - b.cost);
        
        dist[start][0] = 0;
        pq.add(new Edge(start,0,0));

        while(!pq.isEmpty()){
            Edge cur = pq.poll();

            if(dist[cur.to][cur.cnt] < cur.cost) continue;

            for(Edge next : adjLists[cur.to]){
                int newCost = cur.cost + next.cost;
                int nextCnt = cur.cnt + 1;
                
                if(nextCnt <= N && dist[next.to][nextCnt] > newCost){
                    dist[next.to][nextCnt] = newCost;
                    pq.offer(new Edge(next.to, nextCnt, newCost));
                }
            }
        }
    }
}

```
