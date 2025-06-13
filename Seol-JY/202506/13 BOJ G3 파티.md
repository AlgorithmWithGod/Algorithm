```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M, X;
    static ArrayList<ArrayList<Node>> graph;
    static ArrayList<ArrayList<Node>> reverseGraph;
    static int[] distToX;
    static int[] distFromX;
    
    static class Node {
        int vertex;
        int cost;
        
        Node(int vertex, int cost) {
            this.vertex = vertex;
            this.cost = cost;
        }
    }
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        
        graph = new ArrayList<>();
        reverseGraph = new ArrayList<>();
        
        for (int i = 0; i <= N; i++) {
            graph.add(new ArrayList<>());
            reverseGraph.add(new ArrayList<>());
        }
        
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            int time = Integer.parseInt(st.nextToken());
            
            graph.get(start).add(new Node(end, time));
            reverseGraph.get(end).add(new Node(start, time));
        }
        
        distToX = new int[N + 1];
        distFromX = new int[N + 1];
        
        dijkstra(X, graph, distFromX);
        dijkstra(X, reverseGraph, distToX);
        
        int maxTime = 0;
        for (int i = 1; i <= N; i++) {
            if (i != X) {
                maxTime = Math.max(maxTime, distToX[i] + distFromX[i]);
            }
        }
        
        System.out.println(maxTime);
    }
    
    static void dijkstra(int start, ArrayList<ArrayList<Node>> targetGraph, int[] dist) {
        Arrays.fill(dist, Integer.MAX_VALUE);
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> Integer.compare(a.cost, b.cost));
        
        dist[start] = 0;
        pq.offer(new Node(start, 0));
        
        while (!pq.isEmpty()) {
            Node current = pq.poll();
            int currentVertex = current.vertex;
            int currentCost = current.cost;
            
            if (currentCost > dist[currentVertex]) continue;
            
            for (Node next : targetGraph.get(currentVertex)) {
                int nextVertex = next.vertex;
                int nextCost = currentCost + next.cost;
                
                if (nextCost < dist[nextVertex]) {
                    dist[nextVertex] = nextCost;
                    pq.offer(new Node(nextVertex, nextCost));
                }
            }
        }
    }
}
```
