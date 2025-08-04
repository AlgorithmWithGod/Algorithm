```java
import java.util.*;
import java.io.*;

public class boj14567 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int M = nextInt();
        List<List<Integer>> graph = new ArrayList<>();
        Queue<Integer> q = new LinkedList<>();
        int[] degree = new int[N+1];
        int[] answer = new int[N+1];

        for (int i = 0; i <= N; i++) graph.add(new ArrayList<>());
        for (int i = 0; i < M; i++) {
            nextLine();
            int a = nextInt();
            int b = nextInt();
            graph.get(a).add(b);
            degree[b]++;
        }
        for (int i = 1; i <= N; i++) if (degree[i] == 0) q.offer(i);
        int cnt = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                int cur = q.poll();
                answer[cur] = cnt;
                for (int next : graph.get(cur)) {
                    if (--degree[next] == 0) q.offer(next);
                }
            }
            cnt++;
        }
        for (int i = 1; i <= N; i++) System.out.print(answer[i] + " ");
    }
}
```
