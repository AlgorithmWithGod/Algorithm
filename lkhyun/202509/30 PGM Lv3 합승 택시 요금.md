```java
import java.util.*;

class Solution {
    static class Edge{
        int to,cost;
        Edge(int to, int cost){
            this.to = to;
            this.cost = cost;
        }
    }
    static List<Edge>[] adjList;
    static int[] distA;
    static int[] distB;
    static int[] distS;
    public int solution(int n, int s, int a, int b, int[][] fares) {
        int answer = 0;
        adjList = new List[n+1];
        for(int i = 1; i<=n; i++){
            adjList[i] = new ArrayList<>();
        }
        
        for(int[] fare : fares){
            adjList[fare[0]].add(new Edge(fare[1],fare[2]));
            adjList[fare[1]].add(new Edge(fare[0],fare[2]));
        }
        
        distA = new int[n+1];
        distB = new int[n+1];
        distS = new int[n+1];
        dijkstra(a,distA);
        dijkstra(b,distB);
        dijkstra(s,distS);
        
        answer = distS[a] + distS[b];
        for(int i=1; i<=n; i++){
            answer = Math.min(answer, distS[i] + distA[i] + distB[i]);
        }
        return answer;
    }
    public void dijkstra(int start, int[] dist){
        PriorityQueue<Edge> pq = new PriorityQueue<>((a,b) -> Integer.compare(a.cost,b.cost));
        Arrays.fill(dist, Integer.MAX_VALUE);
        pq.offer(new Edge(start,0));
        dist[start] = 0;
        
        while(!pq.isEmpty()){
            Edge cur = pq.poll();
            
            if(dist[cur.to] < cur.cost) continue;
            
            for(Edge next : adjList[cur.to]){
                int newDist = cur.cost + next.cost;
                if(newDist < dist[next.to]){
                    dist[next.to] = newDist;
                    pq.offer(new Edge(next.to,newDist));
                }
            }
        }
    }
}
```
