```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] edges;
    private static BitSet[] tubes;
    private static Set<Integer> start, end;
    private static boolean[] visited;
    private static int N, K, M;

    public static void main(String[] args) throws IOException {
        init();
        int answer = N!=1 ? BFS() : 1;

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        edges = new List[M];
        tubes = new BitSet[M];
        visited = new boolean[M];
        start = new HashSet<>();
        end = new HashSet<>();

        for (int i = 0; i < M; i++) {
            edges[i] = new ArrayList<>();
            tubes[i] = new BitSet();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < K; j++) {
                int num = Integer.parseInt(st.nextToken());
                tubes[i].set(num);
                if (num == 1) start.add(i);
                if (num == N) end.add(i);
            }
        }

        for (int i = 0; i < M-1; i++) {
            for (int j = i+1; j < M; j++) {
                if (tubes[i].intersects(tubes[j])) {
                    edges[i].add(j);
                    edges[j].add(i);
                }
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = -1;
        for (int s : start) {
            visited[s] = true;
            q.add(new int[]{s, 2});
        }

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (end.contains(current[0])) {
                result = current[1];
                break;
            }

            for (int next : edges[current[0]]) {
                if (visited[next]) continue;
                visited[next] = true;
                q.add(new int[]{next, current[1]+1});
            }
        }

        return result;
    }
}
```
