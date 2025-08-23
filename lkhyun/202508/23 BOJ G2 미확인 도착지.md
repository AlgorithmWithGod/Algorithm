```java
import java.util.*;
import java.io.*;

public class Main{
    static class Edge {
        int to;
        int cost;
        
        public Edge(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }
    }
    
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int repeat = Integer.parseInt(br.readLine());
        for(int test=0; test<repeat; test++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            int m = Integer.parseInt(st.nextToken());
            int t = Integer.parseInt(st.nextToken());
            
            List<Edge>[] graph = new ArrayList[n+1];
            for(int i=1; i<=n; i++) {
                graph[i] = new ArrayList<>();
            }
            
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int x1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            
            for(int i=0; i<m; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                int c = Integer.parseInt(st.nextToken());
                if((a == x1 && b == x2) || (a == x2 && b == x1)){
                    graph[a].add(new Edge(b, c*2 - 1));
                    graph[b].add(new Edge(a, c*2 - 1));
                }else{
                    graph[a].add(new Edge(b, c*2));
                    graph[b].add(new Edge(a, c*2));
                }
            }
            
            int[] ends = new int[t];
            for(int i=0; i<t; i++) {
                ends[i] = Integer.parseInt(br.readLine());
            }
            
            int[] dist = new int[n+1];
            Arrays.fill(dist, (int)1e9);
            PriorityQueue<Edge> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
            pq.offer(new Edge(start, 0));
            dist[start] = 0;
            
            while(!pq.isEmpty()) {
                Edge current = pq.poll();

                if(dist[current.to] < current.cost) continue;
                
                for(Edge edge : graph[current.to]) {
                    int newCost = current.cost + edge.cost;
                    if(dist[edge.to] <= newCost) continue;
                    dist[edge.to] = newCost;
                    pq.offer(new Edge(edge.to, newCost));
                }
            }
            Arrays.sort(ends);
            for(int end : ends) {
                int cost = dist[end];
                if(cost%2 == 0) continue;
                sb.append(end).append(" ");
            }
            sb.append("\n");
        }
        
        
        System.out.println(sb.toString().trim());
    }
}
```
