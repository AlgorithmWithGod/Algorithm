```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class BJ_2668_숫자고르기 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder  sb = new StringBuilder();

    private static int           N;
    private static int[]         arr;
    private static boolean[]     visited;
    private static List<Integer> result;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N + 1];

        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        visited = new boolean[N + 1];
        result = new ArrayList<>();
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= N; i++) {
            visited[i] = true;
            dfs(i, i);
            visited[i] = false;
        }
        Collections.sort(result);

        sb.append(result.size()).append("\n");
        for (int num : result) {
            sb.append(num).append("\n");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static void dfs(int start, int cur) {
        int next = arr[cur];

        if (next == start) {
            result.add(start);
            return;
        }

        if (!visited[next]) {
            visited[next] = true;
            dfs(start, next);
            visited[next] = false;
        }
    }

}
```