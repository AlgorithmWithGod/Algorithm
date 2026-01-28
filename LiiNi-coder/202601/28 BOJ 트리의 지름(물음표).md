```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.Queue;
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        solve(n, k);
    }

    private static void solve(int n, int k) {
        Queue<Integer> q = new LinkedList<Integer>();
        q.offer(1);
        int next = 2;
        int edgeCount = 0;
        while (!q.isEmpty() && next <= n) {
            int current = q.poll();
            for (int i = 0; i < k && next <= n; i++) {
                System.out.println(current + " " + next);
                q.offer(next);
                next++;
                edgeCount++;

                
                if (edgeCount == n - 1) {
                    return;
                }
            }
        }
    }
}

```
