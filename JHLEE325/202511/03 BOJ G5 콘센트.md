```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        Integer[] times = new Integer[N];
        for (int i = 0; i < N; i++) {
            times[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(times, Collections.reverseOrder());

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        int initial = Math.min(M, N);
        for (int i = 0; i < initial; i++) {
            pq.offer(times[i]);
        }

        for (int i = initial; i < N; i++) {
            int current = pq.poll();
            current += times[i];
            pq.offer(current);
        }

        int answer = 0;
        while (!pq.isEmpty()) {
            answer = Math.max(answer, pq.poll());
        }

        System.out.println(answer);
    }
}
```
