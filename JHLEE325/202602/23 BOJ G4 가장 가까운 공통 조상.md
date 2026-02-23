```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            int N = Integer.parseInt(br.readLine());
            int[] parent = new int[N + 1];
            boolean[] visited = new boolean[N + 1];

            for (int i = 0; i < N - 1; i++) {
                StringTokenizer st = new StringTokenizer(br.readLine());
                int p = Integer.parseInt(st.nextToken());
                int c = Integer.parseInt(st.nextToken());
                parent[c] = p;
            }

            StringTokenizer st = new StringTokenizer(br.readLine());
            int nodeA = Integer.parseInt(st.nextToken());
            int nodeB = Integer.parseInt(st.nextToken());

            int current = nodeA;
            while (current != 0) {
                visited[current] = true;
                current = parent[current];
            }

            current = nodeB;
            while (current != 0) {
                if (visited[current]) {
                    System.out.println(current);
                    break;
                }
                current = parent[current];
            }
        }
    }
}
```
