```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]>[] edges;
    private static boolean[] visited;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();

        while (M-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());

            bw.write(BFS(start, end) + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        edges = new List[N+1];
        visited = new boolean[N+1];

        for (int i = 1; i <= N; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 0; i < N-1; i++) {
            st =  new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());

            edges[x].add(new int[] {y, d});
            edges[y].add(new int[] {x, d});
        }
    }

    private static int BFS(int start, int end) {
        Queue<int[]> q = new ArrayDeque<>();
        int result = -1;
        Arrays.fill(visited, false);
        visited[start] = true;
        q.add(new int[] {start, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == end) {
                result = current[1];
                break;
            }

            for (int[] edge : edges[current[0]]) {
                if (visited[edge[0]]) continue;

                visited[edge[0]] = true;
                q.add(new int[]{edge[0], current[1]+edge[1]});
            }
        }

        return result;
    }
}
```
