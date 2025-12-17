```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long)3e10 + 5;
    private static List<int[]> edges;
    private static long[] dist;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        boolean result = bellmanFord();

        if (result) bw.write(-1 + "\n");
        else {
            for (int i = 2; i <= N; i++) {
                if (dist[i] != INF) bw.write(dist[i] + "\n");
                else bw.write(-1 + "\n");
            }
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        edges = new ArrayList<>();
        dist = new long[N+1];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int A = Integer.parseInt(st.nextToken());
            int B = Integer.parseInt(st.nextToken());
            int C = Integer.parseInt(st.nextToken());
            edges.add(new int[]{A, B, C});
        }
    }

    private static boolean bellmanFord() {
        Arrays.fill(dist, INF);
        dist[1] = 0;

        for (int i = 0; i < N-1; i++) {
            for (int[] edge : edges) {
                if (dist[edge[0]] != INF && dist[edge[1]] > dist[edge[0]] + edge[2]) {
                    dist[edge[1]] = dist[edge[0]] + edge[2];
                }
            }
        }

        for (int[] edge : edges) {
            if (dist[edge[0]] != INF && dist[edge[1]] > dist[edge[0]] + edge[2]) {
                return true;
            }
        }

        return false;
    }
}
```
