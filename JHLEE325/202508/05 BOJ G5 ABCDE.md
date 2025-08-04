```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m;
    static List<Integer>[] friends;
    static boolean[] visited;
    static boolean found = false;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        friends = new ArrayList[n];
        for (int i = 0; i < n; i++) friends[i] = new ArrayList<>();

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            friends[a].add(b);
            friends[b].add(a);
        }

        visited = new boolean[n];
        for (int i = 0; i < n && !found; i++) {
            visited[i] = true;
            dfs(i, 1);
            visited[i] = false;
        }

        System.out.println(found ? 1 : 0);
    }

    static void dfs(int cur, int depth) {
        if (found) return;
        if (depth == 5) {
            found = true;
            return;
        }

        for (int next : friends[cur]) {
            if (visited[next]) continue;
            visited[next] = true;
            dfs(next, depth + 1);
            visited[next] = false;
            if (found) return;
        }
    }
}

```
