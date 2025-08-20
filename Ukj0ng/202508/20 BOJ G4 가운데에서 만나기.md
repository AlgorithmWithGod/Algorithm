```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Edge>[] graph;
    private static List<Integer> answer;
    private static int[][] dist;
    private static int[] arr;
    private static int N, M, K, min;
    public static void main(String[] args) throws IOException {
        init();
        for (int i = 1; i <= N; i++) {
            dijkstra(i);
        }

        for (int i = 1; i <= N; i++) {
            int max = 0;
            for (int idx = 1; idx <= K; idx++) {
                int j = arr[idx];
                max = Math.max(max, dist[j][i] + dist[i][j]);
            }

            if (max == min) {
                answer.add(i);
            } else if (max < min) {
                min = max;
                answer.clear();
                answer.add(i);
            }
        }

        Collections.sort(answer);

        for (int element : answer) {
            bw.write(element + " ");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        answer = new ArrayList<>();

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            int v = Integer.parseInt(st.nextToken());
            int u = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            graph[v].add(new Edge(u, w));
        }

        K = Integer.parseInt(br.readLine());
        arr = new int[K + 1];
        dist = new int[N + 1][N + 1];
        st = new  StringTokenizer(br.readLine());
        for (int i = 1; i <= K; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        min = Integer.MAX_VALUE - 10;
    }

    private static void dijkstra(int start) {
        PriorityQueue<Edge> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.cost ,o2.cost));
        int[] temp = new int[N + 1];
        Arrays.fill(temp, Integer.MAX_VALUE - 10);
        temp[start] = 0;
        pq.add(new Edge(start, 0));

        while (!pq.isEmpty()) {
            Edge current = pq.poll();

            if (current.cost > temp[current.dest]) continue;

            for (Edge next : graph[current.dest]) {
                int nDest = next.dest;
                int nCost = current.cost + next.cost;

                if (nCost < temp[nDest]) {
                    temp[nDest] = nCost;
                    pq.add(new Edge(nDest, temp[nDest]));
                }
            }
        }

        for (int i = 1; i <= N; i++) {
            dist[start][i] = temp[i];
        }
    }

    static class Edge {
        int dest;
        int cost;
        Edge(int dest, int cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}

```
