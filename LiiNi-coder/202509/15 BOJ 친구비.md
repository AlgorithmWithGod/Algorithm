```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        int[] parent = new int[N + 1];
        int[] cost = new int[N + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            cost[i] = Integer.parseInt(st.nextToken());
            parent[i] = i;
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int pa = find(parent, a);
            int pb = find(parent, b);
            if (pa != pb) {
                if (cost[pa] < cost[pb])
                    parent[pb] = pa;
                else
                    parent[pa] = pb;
            }
        }

        boolean[] visited = new boolean[N + 1];
        
        int total = 0;
        for (int i = 1; i <= N; i++) {
            int p = find(parent, i);
            if (!visited[p]) {
                total += cost[p];
                visited[p] = true;
            }
        }

        if (total <= K)
            System.out.println(total);
        else
            System.out.println("Oh no");
    }

    static int find(int[] parent, int x) {
        if (parent[x] == x)
            return x;
        parent[x] = find(parent, parent[x]);
        return parent[x];
    }
}

```
