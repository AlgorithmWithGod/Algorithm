```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] graph;
    private static int[] nodes;
    private static boolean[] visited;
    private static int N, R, Q;

    public static void main(String[] args) throws IOException {
        init();

        countSubNodes(R);
        while (Q-->0) {
            int q = Integer.parseInt(br.readLine());
            bw.write(nodes[q] + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        graph = new List[N+1];
        nodes = new int[N+1];
        visited = new boolean[N+1];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        Arrays.fill(nodes, 1);

        for (int i = 0; i < N-1; i++) {
            st = new StringTokenizer(br.readLine());
            int U = Integer.parseInt(st.nextToken());
            int V = Integer.parseInt(st.nextToken());

            graph[U].add(V);
            graph[V].add(U);
        }
    }

    private static void countSubNodes(int start) {
        visited[start] = true;

        for (int next : graph[start]) {
            if (visited[next]) continue;
            countSubNodes(next);
            nodes[start] += nodes[next];
        }
    }
}
```
