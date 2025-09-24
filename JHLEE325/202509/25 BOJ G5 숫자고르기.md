```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[] arr;
    static boolean[] visited;
    static Set<Integer> result = new TreeSet<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        n = Integer.parseInt(br.readLine());

        arr = new int[n +1];
        for (int i = 1; i <= n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        for (int i = 1; i <= n; i++) {
            visited = new boolean[n +1];
            dfs(i, i);
        }

        sb.append(result.size()).append("\n");
        for (int x : result) sb.append(x).append("\n");
        System.out.print(sb);
    }

    static void dfs(int start, int cur) {
        if (!visited[cur]) {
            visited[cur] = true;
            dfs(start, arr[cur]);
        } else {
            if (cur == start) {
                result.add(cur);
            }
        }
    }
}
```
