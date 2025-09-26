```
import java.util.*;

class Solution {
    private final int INF = Integer.MAX_VALUE - 10;
    private List<Integer>[] graph;
    private int[] dist;
    
    public int[] solution(int n, int[][] roads, int[] sources, int destination) {
        init(n, roads);
        int[] answer = new int[sources.length];
        
        dijkstra(destination);
        
        for (int i = 0; i < answer.length; i++) {
            int result = dist[sources[i]];
            if (result == INF) answer[i] = -1;
            else answer[i] = result;
        }
        
        return answer;
    }
    
    private void init(int n, int[][] roads) {
        graph = new List[n+1];
        dist = new int[n+1];
        
        for (int i = 0; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }
        
        for (int[] road : roads) {
            graph[road[0]].add(road[1]);
            graph[road[1]].add(road[0]);
        }
    }
    
    private void dijkstra(int start) {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> Long.compare(o1.cost, o2.cost));
        Arrays.fill(dist, INF);
        dist[start] = 0;
        pq.add(new Node(start, dist[start]));
        
        while (!pq.isEmpty()) {
            Node current = pq.poll();
            
            if (current.cost > dist[current.dest]) continue;
            
            for (Integer next : graph[current.dest]) {
                int nCost = 1 + dist[current.dest];
                
                if (nCost < dist[next]) {
                    dist[next] = nCost;
                    pq.add(new Node(next, dist[next]));
                }
            }
        }
    }
    
    class Node {
        int dest;
        int cost;
        
        Node (int dest, int cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}
```
