```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<int[]> pq;
    private static List<int[]>[] edges;
    private static int[] uf, size;
    private static boolean[] visited;
    private static int N, M, K;

    public static void main(String[] args) throws IOException {
        init();
        kruskal();

        while (K-->0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());

            int answer = BFS(start, end);
            bw.write(answer + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        uf = new int[N+1];
        size = new int[N+1];
        visited = new boolean[N+1];
        pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o2[2], o1[2]));
        edges = new List[N+1];

        for (int i = 1; i <= N; i++) {
            uf[i] = i;
            size[i] = 1;
            edges[i] = new ArrayList<>();
        }

        for (int a = 0; a < M; a++) {
             st = new StringTokenizer(br.readLine());
             int i = Integer.parseInt(st.nextToken());
             int j = Integer.parseInt(st.nextToken());
             int w = Integer.parseInt(st.nextToken());
             pq.add(new int[] {i, j, w});
        }
    }

    private static int BFS(int start, int end) {
        Queue<int[]> q = new ArrayDeque<>();
        Arrays.fill(visited, false);
        visited[start] = true;
        q.add(new int[] {start, 200});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == end) {
                return current[1];
            }

            for (int[] edge : edges[current[0]]) {
                if (visited[edge[0]]) continue;
                visited[edge[0]] = true;
                q.add(new int[] {edge[0], Math.min(current[1], edge[1])});
            }
        }

        return -1;
    }

    private static void kruskal() {
        int edgeCount = 0;

        while (!pq.isEmpty() && edgeCount + 1 <= N) {
            int[] edge = pq.poll();

            int i = find(edge[0]);
            int j = find(edge[1]);

            if (i == j) continue;
            union(i, j);
            edges[i].add(new int[]{j, edge[2]});
            edges[j].add(new int[]{i, edge[2]});
            edgeCount++;
        }
    }

    private static void union(int x, int y) {
        int X = find(x);
        int Y = find(y);

        if (size[X] < size[Y]) {
            uf[X] = Y;
            size[Y] += size[X];
        } else {
            uf[Y] = X;
            size[X] += size[Y];
        }
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
