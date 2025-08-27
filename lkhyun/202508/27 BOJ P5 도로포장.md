```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,M,K;
    static class Edge{
        int to,cost;

        Edge(int to, int cost){
            this.to = to;
            this.cost = cost;
        }
    }
    static class State{
        int to,k;
        long cost;
        State(int to, int k, long cost){
            this.to = to;
            this.k = k;
            this.cost = cost;
        }
    }
    static List<Edge>[] adjList;
    
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        adjList = new ArrayList[N+1];

        for (int i = 1; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            adjList[from].add(new Edge(to, cost));
            adjList[to].add(new Edge(from, cost));
        }
        long[][] dist = dijkstra();
        long ans = Long.MAX_VALUE;
        for (int i = 0; i <= K; i++) {
            ans = Math.min(ans, dist[N][i]);
        }
        bw.write(ans+"");
        bw.close();
    }
    public static long[][] dijkstra(){
        PriorityQueue<State> pq = new PriorityQueue<>((a,b) -> Long.compare(a.cost,b.cost));
        long[][] dist = new long[N+1][K+1];
        for (int i = 1; i <= N; i++) {
            Arrays.fill(dist[i],Long.MAX_VALUE);
        }
        pq.offer(new State(1,0,0));
        dist[1][0] = 0;

        while(!pq.isEmpty()){
            State cur = pq.poll();

            if(dist[cur.to][cur.k] < cur.cost) continue;
            
            for(Edge e : adjList[cur.to]){
                long notUsedCost = cur.cost + e.cost;
                long usedCost = cur.cost;

                if(notUsedCost < dist[e.to][cur.k]){
                    dist[e.to][cur.k] = notUsedCost;
                    pq.offer(new State(e.to, cur.k, notUsedCost));
                }

                if(cur.k < K && usedCost < dist[e.to][cur.k + 1]){
                    dist[e.to][cur.k + 1] = usedCost;
                    pq.offer(new State(e.to, cur.k + 1, usedCost));
                }
            }
        }
        return dist;
    }
}
```
