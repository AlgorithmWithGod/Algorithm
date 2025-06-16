```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    private static int N;
    private static List<Node>[] graph;
    private static boolean[] visited;
    private static int maxDistance;
    private static int farthestNode;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        N = Integer.parseInt(br.readLine());
        graph = new List[N + 1];
        
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }
        
        for (int i = 0; i < N - 1; i++) {
            st = new StringTokenizer(br.readLine());
            
            int parent = Integer.parseInt(st.nextToken());
            int child = Integer.parseInt(st.nextToken());
            int weight = Integer.parseInt(st.nextToken());

            graph[parent].add(new Node(child, weight));
            graph[child].add(new Node(parent, weight));
        }

        visited = new boolean[N + 1];
        maxDistance = 0;
        farthestNode = 1;
        dfs(1, 0);
        
        visited = new boolean[N + 1];
        maxDistance = 0;
        dfs(farthestNode, 0);

        System.out.println(maxDistance);
    }

    private static void dfs(int node, int distance) {
        visited[node] = true;
        
        if (distance > maxDistance) {
            maxDistance = distance;
            farthestNode = node;
        }

        for (Node next : graph[node]) {
            if (!visited[next.to]) {
                dfs(next.to, distance + next.weight);
            }
        }
    }

    static class Node {
        int to;
        int weight;

        Node(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
    }
}
```
