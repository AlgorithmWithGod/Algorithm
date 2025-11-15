```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = Integer.MAX_VALUE/2;
    private static List<Edge>[] edges;
    private static Map<String, Integer> visited;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        int answer = dijkstra();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        edges = new List[N];
        visited = new HashMap<>();

        for (int i = 0; i < N; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 0; i < N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 0; j < N; j++) {
                 if (input[j] == '.') continue;
                 edges[i].add(new Edge(j, input[j] - '0'));
            }
        }

        for (int i = 0; i < N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 0; j < N; j++) {
                if (input[j] == '.') continue;
                for (int k = 0; k < edges[i].size(); k++) {
                    if (j == edges[i].get(k).dest) {
                        edges[i].get(k).w2 = input[j] - '0';
                    }
                }
            }
        }
    }

    private static int dijkstra() {
        PriorityQueue<Edge> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
        pq.add(new Edge(0, 0, 0, 0));

        while (!pq.isEmpty()) {
            Edge current = pq.poll();

            String currentKey = current.dest + "," + current.w1 + "," + current.w2;
            if (visited.containsKey(currentKey)) continue;
            visited.put(currentKey, current.cost);

            if (current.dest == 1) {
                return current.cost;
            }

            for (Edge edge : edges[current.dest]) {
                int w1 = current.w1 + edge.w1;
                int w2 = current.w2 + edge.w2;
                int nCost = w1 * w2;

                String key = edge.dest + "," + w1 + "," + w2;

                if (!visited.containsKey(key) || visited.get(key) > nCost) {
                    pq.add(new Edge(edge.dest, w1, w2, nCost));
                }
            }
        }

        return -1;
    }

    static class Edge {
        int dest;
        int w1;
        int w2;
        int cost;

        public Edge(int dest, int w1) {
            this.dest = dest;
            this.w1 = w1;
            this.w2 = 0;
            this.cost = 0;
        }

        public Edge(int dest, int w1, int w2, int cost) {
            this.dest = dest;
            this.w1 = w1;
            this.w2 = w2;
            this.cost = cost;
        }
    }
}
```
