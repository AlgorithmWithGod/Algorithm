```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int dnode;
    static List<Integer>[] tree;
    static boolean[] visited;
    static int leafcount = 0;
    static int root;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        tree = new ArrayList[N];
        visited = new boolean[N];
        for (int i = 0; i < N; i++) {
            tree[i] = new ArrayList<>();
        }

        StringTokenizer st = new StringTokenizer(br.readLine());
        root = -1;
        for (int i = 0; i < N; i++) {
            int parent = Integer.parseInt(st.nextToken());
            if (parent == -1) {
                root = i;
            } else {
                tree[parent].add(i);
            }
        }

        dnode = Integer.parseInt(br.readLine());

        if (dnode == root) {
            System.out.println(0);
            return;
        }

        dfs(root);
        System.out.println(leafcount);
    }

    static void dfs(int now) {
        visited[now] = true;
        int childCount = 0;

        for (int next : tree[now]) {
            if (next == dnode) continue;
            if (!visited[next]) {
                dfs(next);
                childCount++;
            }
        }

        if (childCount == 0) {
            leafcount++;
        }
    }
}
```
