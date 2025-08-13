```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    private static BufferedReader br;
    private static StringTokenizer st;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        Queue<Integer> q = new LinkedList<>();
        HashSet<Integer> visited = new HashSet<>();
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            int x = Integer.parseInt(st.nextToken());
            q.offer(x);
            visited.add(x);
        }

        long answer = 0;
        int distance = 1;
        int builtCount = 0;
        int[] dxs = { -1, 1 };

        outer: // naming가능한 break문
        while (!q.isEmpty()) {
            int size = q.size();
            for (int t = 0; t < size; t++) {
                int x = q.poll();
                for (int d : dxs) {
                    int nx = x + d;
                    if (visited.contains(nx))
                        continue;
                    visited.add(nx);
                    q.offer(nx);
                    answer += distance;
                    builtCount++;
                    if (builtCount == k)
                        break outer;
                }
            }
            distance++;
        }
        System.out.println(answer);
        br.close();
    }
}
```
