```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] edges;
    private static int[] parent;
    private static int N, M, answer;
    public static void main(String[] args) throws IOException {
        init();

        for (int i = 0; i < N; i++) {
            if (parent[i] == -1 && i != M) {
                DFS(i);
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        StringTokenizer st = new StringTokenizer(br.readLine());
        parent = new int[N];
        edges = new List[N];

        for (int i = 0; i < N; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 0; i < N; i++) {
            parent[i] = Integer.parseInt(st.nextToken());
            if (parent[i] == -1) continue;
            edges[parent[i]].add(i);
        }

        M = Integer.parseInt(br.readLine());
    }

    private static void DFS(int start) {
        if (isLeaf(start)) {
            answer++;
            return;
        }

        for (int next : edges[start]) {
            if (next == M) continue;
            DFS(next);
        }
    }

    private static boolean isLeaf(int node) {
        if (edges[node].isEmpty()) {
            return true;
        }

        if (edges[node].size() == 1 && edges[node].get(0) == M) {
            return true;
        }

        return false;
    }
}
```
