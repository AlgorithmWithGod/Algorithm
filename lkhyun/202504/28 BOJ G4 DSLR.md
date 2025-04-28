```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws Exception {
        int T = Integer.parseInt(br.readLine());
        while (T-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int A = Integer.parseInt(st.nextToken());
            int B = Integer.parseInt(st.nextToken());
            bfs(A, B);
        }
        bw.flush();
        bw.close();
    }

    static void bfs(int start, int target) throws IOException {
        boolean[] visited = new boolean[10000];
        int[] prev = new int[10000];
        char[] op = new char[10000];

        ArrayDeque<Integer> q = new ArrayDeque<>();
        visited[start] = true;
        q.add(start);

        while (!q.isEmpty()) {
            int cur = q.poll();
            if (cur == target) break;

            // D
            int next = (cur * 2) % 10000;
            if (!visited[next]) {
                visited[next] = true;
                prev[next] = cur;
                op[next] = 'D';
                q.add(next);
            }
            // S
            next = (cur == 0 ? 9999 : cur - 1);
            if (!visited[next]) {
                visited[next] = true;
                prev[next] = cur;
                op[next] = 'S';
                q.add(next);
            }
            // L
            next = (cur % 1000) * 10 + cur / 1000;
            if (!visited[next]) {
                visited[next] = true;
                prev[next] = cur;
                op[next] = 'L';
                q.add(next);
            }
            // R
            next = (cur % 10) * 1000 + cur / 10;
            if (!visited[next]) {
                visited[next] = true;
                prev[next] = cur;
                op[next] = 'R';
                q.add(next);
            }
        }

        StringBuilder sb = new StringBuilder();
        for (int p = target; p != start; p = prev[p]) {
            sb.append(op[p]);
        }
        bw.write(sb.reverse().toString());
        bw.write('\n');
    }
}


```
