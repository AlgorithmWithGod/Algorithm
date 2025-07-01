```java
import java.io.*;
import java.util.*;

public class Main {
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int TC = nextInt(new StringTokenizer(br.readLine()));
        
        while (TC-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int N = nextInt(st);
            int M = nextInt(st);
            int W = nextInt(st);
            
            List<Edge>[] graph = new ArrayList[N + 1];
            for (int i = 1; i <= N; i++) {
                graph[i] = new ArrayList<>();
            }
            
            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int s = nextInt(st);
                int e = nextInt(st);
                int t = nextInt(st);
                
                graph[s].add(new Edge(e, t));
                graph[e].add(new Edge(s, t));
            }
            
            for (int i = 0; i < W; i++) {
                st = new StringTokenizer(br.readLine());
                int s = nextInt(st);
                int e = nextInt(st);
                int t = nextInt(st);
                
                graph[s].add(new Edge(e, -t));
            }
            
            if (hasNegativeCycle(graph, N)) {
                System.out.println("YES");
            } else {
                System.out.println("NO");
            }
        }
    }
    
    static boolean hasNegativeCycle(List<Edge>[] graph, int N) {
        long[] dist = new long[N + 1];
        final long INF = 987654321
        Arrays.fill(dist, INF);
        
        for (int start = 1; start <= N; start++) {
            if (dist[start] != INF) continue;
            
            dist[start] = 0;
            
            boolean updated = false;
            for (int i = 0; i < N - 1; i++) {
                updated = false;
                for (int j = 1; j <= N; j++) {
                    if (dist[j] == INF) continue;
                    
                    for (Edge edge : graph[j]) {
                        if (dist[j] + edge.cost < dist[edge.to]) {
                            dist[edge.to] = dist[j] + edge.cost;
                            updated = true;
                        }
                    }
                }
                if (!updated) break;
            }
            
            for (int j = 1; j <= N; j++) {
                if (dist[j] == INF) continue;
                
                for (Edge edge : graph[j]) {
                    if (dist[j] + edge.cost < dist[edge.to]) {
                        return true;
                    }
                }
            }
        }
        
        return false;
    }

    static class Edge {
        int to, cost;
        
        Edge(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }
    }
    
    static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
