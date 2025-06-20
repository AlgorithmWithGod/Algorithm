```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int N, M, K;
    static int[] prices;
    static int[] parent;
    static int[] minCost;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = nextInt(st);
        M = nextInt(st);
        K = nextInt(st);

        prices = new int[N + 1];
        parent = new int[N + 1];
        minCost = new int[N + 1];
        
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            prices[i] = nextInt(st);
            parent[i] = i;
            minCost[i] = prices[i];
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            union(nextInt(st), nextInt(st));
        }
        
        for (int i = 1; i <= N; i++) {
            int root = find(i);
            minCost[root] = Math.min(minCost[root], prices[i]);
        }
        
        int totalCost = 0;
        boolean[] visited = new boolean[N + 1];
        
        for (int i = 1; i <= N; i++) {
            int root = find(i);
            if (!visited[root]) {
                visited[root] = true;
                totalCost += minCost[root];
            }
        }
        if (totalCost <= K) {
            System.out.println(totalCost);
        } else {
            System.out.println("Oh no");
        }
    }
    
    private static int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        
        return parent[x];
    }
    
    private static void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            parent[rootY] = rootX;
        }
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
