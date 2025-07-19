```java
import java.util.*;
import java.io.*;

public class Main{
    static class Edge{
        int v,w;
        Edge(int v,int w){
            this.v=v;
            this.w=w;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static List<Edge>[] edges;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        edges = new List[N+1];
        for (int i = 1; i <= N; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            edges[u].add(new Edge(v,w));
        }

        st = new StringTokenizer(br.readLine());
        int start = Integer.parseInt(st.nextToken());
        int middle = Integer.parseInt(st.nextToken());
        int end = Integer.parseInt(st.nextToken());

        int[] dist1 = new int[N+1];
        int[] dist2 = new int[N+1];
        int[] dist3 = new int[N+1];
        dijkstra(start,dist1);
        dijkstra(middle,dist2);
        if(dist1[middle] == Integer.MAX_VALUE || dist2[end] == Integer.MAX_VALUE){
            bw.write("-1 ");
        }else{
            bw.write(dist1[middle] + dist2[end] + " ");
        }
        dijkstra2(start,middle,dist3);
        if(dist3[end] == Integer.MAX_VALUE){
            bw.write("-1 ");
        }else{
            bw.write(dist3[end]+"");
        }
        bw.close();
    }
    static void dijkstra(int start, int[] dist){
        PriorityQueue<Edge> pq = new PriorityQueue<>((a,b) -> a.w - b.w);
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;
        pq.add(new Edge(start,0));

        while(!pq.isEmpty()){
            Edge cur = pq.poll();

            if(dist[cur.v] < cur.w) continue;

            for (Edge edge : edges[cur.v]) {
                int newDist = cur.w + edge.w;
                if(newDist < dist[edge.v]){
                    dist[edge.v] = newDist;
                    pq.offer(new Edge(edge.v, newDist));
                }
            }
        }
    }
    static void dijkstra2(int start, int noAccess, int[] dist){
        PriorityQueue<Edge> pq = new PriorityQueue<>((a,b) -> a.w - b.w);
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;
        pq.add(new Edge(start,0));

        while(!pq.isEmpty()){
            Edge cur = pq.poll();

            if(dist[cur.v] < cur.w) continue;

            for (Edge edge : edges[cur.v]) {
                if(edge.v == noAccess) continue;
                int newDist = cur.w + edge.w;
                if(newDist < dist[edge.v]){
                    dist[edge.v] = newDist;
                    pq.offer(new Edge(edge.v, newDist));
                }
            }
        }
    }
}
```
