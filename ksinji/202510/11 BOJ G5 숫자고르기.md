```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int[] num;
    static boolean[] visited;
    static boolean[] finished;
    static List<Integer> result = new ArrayList<>();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        num = new int[N + 1];
        visited = new boolean[N + 1];
        finished = new boolean[N + 1];

        for (int i = 1; i <= N; i++) {
            num[i] = Integer.parseInt(br.readLine());
        }

        for (int i = 1; i <= N; i++) {
            if (!visited[i]) dfs(i);
        }

        Collections.sort(result);
        StringBuilder sb = new StringBuilder();
        sb.append(result.size()).append('\n');
        for (int x : result) {
            sb.append(x).append('\n');
        }
        System.out.print(sb);
    }

    static void dfs(int x) {
        visited[x] = true;
        int y = num[x];

        if (!visited[y]) {
            dfs(y);
        } else if (!finished[y]) {
            // 사이클이 존재할 경우
            int cur = y;
            do {
                result.add(cur); // 사이클에 포함되는 노드 result에 추가
                cur = num[cur];
            } while (cur != y);
        }

        finished[x] = true;
    }
}
```
