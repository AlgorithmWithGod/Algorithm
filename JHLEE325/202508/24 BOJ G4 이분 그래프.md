```java
import java.io.*;
import java.util.*;

public class Main {

    static ArrayList<Integer>[] graph;
    static int[] color;
    static int v, e;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();
        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            st = new StringTokenizer(br.readLine());
            v = Integer.parseInt(st.nextToken());
            e = Integer.parseInt(st.nextToken());

            graph = new ArrayList[v + 1];
            for (int i = 1; i <= v; i++) graph[i] = new ArrayList<>();

            for (int i = 0; i < e; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                graph[a].add(b);
                graph[b].add(a);
            }

            color = new int[v + 1];
            boolean ok = true;

            for (int i = 1; i <= v && ok; i++) {
                if (color[i] == 0) {
                    ok = bfs(i);
                }
            }

            if(ok){
                sb.append("YES\n");
            }
            else{
                sb.append("NO\n");
            }
        }

        System.out.print(sb.toString());
    }

    static boolean bfs(int s) {
        ArrayDeque<Integer> q = new ArrayDeque<>();
        color[s] = 1;
        q.offer(s);

        while (!q.isEmpty()) {
            int u = q.poll();
            int nextColor = -color[u];

            for (int v : graph[u]) {
                if (color[v] == 0) {
                    color[v] = nextColor;
                    q.offer(v);
                } else if (color[v] == color[u]) {
                    return false;
                }
            }
        }
        return true;
    }
}

```
