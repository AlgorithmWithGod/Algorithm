```java
import java.util.*;
class Solution {
    static class Node implements Comparable<Node> {
        int v, w;

        public Node(int v, int w) {
            this.v = v;
            this.w = w;
        }
        
        @Override
        public int compareTo(Node other) {
            return Integer.compare(this.w, other.w);
        }
    }
    
    public int solution(int N, int[][] road, int K) {        
        ArrayList<ArrayList<Node>> graph = new ArrayList<>();
        for (int i = 0; i <= N; i++) {
            graph.add(new ArrayList<>());
        }
        
        for (int i = 0; i < road.length; i++) {
            int u = road[i][0];
            int v = road[i][1];
            int w = road[i][2];
            
            graph.get(u).add(new Node(v, w));
            graph.get(v).add(new Node(u, w));
        }
        
        int[] dist = new int[N+1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[1] = 0;
        
        PriorityQueue<Node> q = new PriorityQueue<>();
        q.add(new Node(1, 0));
        
        while (!q.isEmpty()) {
            Node current = q.remove();
            
            if (current.w > dist[current.v]) continue;
            
            for (Node next : graph.get(current.v)) {
                int cost = next.w + dist[current.v];
                
                if (cost < dist[next.v]) {
                    dist[next.v] = cost;
                    q.add(new Node(next.v, cost));
                }
            }
        }

        int answer = 0;
        for (int i = 1; i <= N; i++) {
            if (dist[i] <= K) answer++;
        }
        return answer;
    }
}
```
