```java
import java.io.*;
import java.util.*;

public class Main {
    static int[] parent;
    static int[] count;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        while (T-- > 0) {
            int F = Integer.parseInt(br.readLine());

            parent = new int[F * 2];
            count = new int[F * 2];
            for (int i = 0; i < F * 2; i++) {
                parent[i] = i;
                count[i] = 1;
            }

            Map<String, Integer> map = new HashMap<>();
            int id = 0;

            for (int i = 0; i < F; i++) {
                StringTokenizer st = new StringTokenizer(br.readLine());
                String f1 = st.nextToken();
                String f2 = st.nextToken();

                if (!map.containsKey(f1)) map.put(f1, id++);
                if (!map.containsKey(f2)) map.put(f2, id++);

                sb.append(union(map.get(f1), map.get(f2))).append("\n");
            }
        }
        System.out.print(sb.toString());
    }

    static int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    static int union(int x, int y) {
        x = find(x);
        y = find(y);

        if (x != y) {
            parent[y] = x;
            count[x] += count[y];
        }

        return count[x];
    }
}
```
