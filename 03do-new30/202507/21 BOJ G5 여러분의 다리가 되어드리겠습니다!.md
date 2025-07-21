```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static List<Integer>[] graph;
    static int[] parents;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        graph = new List[N+1];
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }
        makeParents();
        for (int i = 0; i < N-2; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph[a].add(b);
            graph[b].add(a);
            union(a, b);
        }
        boolean found = false;
        for (int i = 1; i < N; i++) {
            if (found) break;
            for (int j = i + 1; j <= N; j++) {
                if (find(i) == find(j)) {
                    continue;
                }
                System.out.println(i + " " + j);
                found = true;
                break;
            }
        }
        br.close();

    }

    static void makeParents() {
        parents = new int[N+1];
        for (int i = 1; i <= N; i++) {
            parents[i] = i;
        }
    }

    static int find(int a) {
        if (parents[a] == a) {return a;}
        return parents[a] = find(parents[a]);
    }

    static boolean union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);
        if (rootA == rootB) {return false;}
        if (rootA < rootB) {
            parents[rootB] = rootA;
        } else {
            parents[rootA] = rootB;
        }
        return true;
    }
}
```
