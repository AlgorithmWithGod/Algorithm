```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr;
    private static boolean[] visited;
    private static Set<Integer> result;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        result = new TreeSet<>();
        visited = new boolean[N + 1];

        for (int i = 1; i <= N; i++) {
            if (!visited[i]) {
                DFS(i, i, new HashSet<>());
            }
        }

        bw.write(result.size() + "\n");
        for (int num : result) {
            bw.write(num + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N + 1];

        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
    }

    private static void DFS(int current, int start, Set<Integer> path) {
        if (visited[current]) return;

        if (current == start && !path.isEmpty()) {
            result.addAll(path);
            for (int node : path) {
                visited[node] = true;
            }
            return;
        }

        if (path.contains(current)) {
            return;
        }

        path.add(current);
        DFS(arr[current], start, path);
        path.remove(current);
    }
}
```
