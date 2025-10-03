```
import java.io.*;
import java.util.*;

public class Main {
    static class Node {
        int to, cost;
        Node(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int Q = Integer.parseInt(st.nextToken());

        List<Node>[] graph = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++) graph[i] = new ArrayList<>();

        for (int i = 0; i < N - 1; i++) {
            st = new StringTokenizer(br.readLine());
            int p = Integer.parseInt(st.nextToken());
            int q = Integer.parseInt(st.nextToken());
            int r = Integer.parseInt(st.nextToken());
            graph[p].add(new Node(q, r));
            graph[q].add(new Node(p, r));
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < Q; i++) {
            st = new StringTokenizer(br.readLine());
            int k = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());

            boolean[] visited = new boolean[N + 1];
            Queue<Integer> q = new LinkedList<>();
            visited[v] = true;
            q.add(v);
            int count = 0;

            while (!q.isEmpty()) {
                int cur = q.poll();
                for (Node nxt : graph[cur]) {
                    if (!visited[nxt.to] && nxt.cost >= k) {
                        visited[nxt.to] = true;
                        q.add(nxt.to);
                        count++;
                    }
                }
            }
            sb.append(count).append("\n");
        }

        System.out.print(sb);
    }
}
```
