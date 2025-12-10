```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M, K;
    static int[] cost;
    static List<Integer>[] graph;
    static boolean[] visited;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        cost = new int[N + 1];
        visited = new boolean[N + 1];
        graph = new ArrayList[N + 1];

        for (int i = 1; i <= N; i++) graph[i] = new ArrayList<>();

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            cost[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph[a].add(b);
            graph[b].add(a);
        }

        int totalCost = 0;

        for (int i = 1; i <= N; i++) {
            if (!visited[i]) {
                int minCost = bfs(i);
                totalCost += minCost;

                if (totalCost > K) {
                    System.out.println("Oh no");
                    return;
                }
            }
        }

        System.out.println(totalCost);
    }

    static int bfs(int start) {
        Queue<Integer> q = new ArrayDeque<>();
        q.add(start);
        visited[start] = true;

        int minCost = cost[start];

        while (!q.isEmpty()) {
            int cur = q.poll();
            minCost = Math.min(minCost, cost[cur]);

            for (int next : graph[cur]) {
                if (!visited[next]) {
                    visited[next] = true;
                    q.offer(next);
                }
            }
        }
        return minCost;
    }
}

```
