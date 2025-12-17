```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static ArrayList<Integer>[] adj;
    static int[] colors;
    static boolean isPossible;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());

            adj = new ArrayList[N + 1];
            for (int i = 1; i <= N; i++) {
                adj[i] = new ArrayList<>();
            }
            colors = new int[N + 1];
            isPossible = true;

            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int u = Integer.parseInt(st.nextToken());
                int v = Integer.parseInt(st.nextToken());

                adj[u].add(v);
                adj[v].add(u);
            }

            for (int i = 1; i <= N; i++) {
                if (!isPossible) break;

                if (colors[i] == 0) {
                    bfs(i);
                }
            }

            if (isPossible) {
                System.out.println("possible");
            } else {
                System.out.println("impossible");
            }
        }
    }

    private static void bfs(int startNode) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(startNode);
        colors[startNode] = 1;

        while (!queue.isEmpty()) {
            int current = queue.poll();

            for (int next : adj[current]) {
                if (colors[next] == 0) {
                    colors[next] = 3 - colors[current];
                    queue.add(next);
                }
                else if (colors[next] == colors[current]) {
                    isPossible = false;
                    return;
                }
            }
        }
    }
}```
