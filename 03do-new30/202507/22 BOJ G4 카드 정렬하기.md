```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 0; i < N; i++) {
            pq.offer(Integer.parseInt(br.readLine()));
        }
        int sum = 0;
        while (pq.size() >= 2) {
            int a = pq.poll();
            int b = pq.poll();
            pq.offer(a + b);
            sum += a + b;
        }
        System.out.println(sum);
        br.close();
    }
}
```
