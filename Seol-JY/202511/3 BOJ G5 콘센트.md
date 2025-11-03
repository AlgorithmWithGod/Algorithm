```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] firstLine = br.readLine().split(" ");
        int N = Integer.parseInt(firstLine[0]);
        int M = Integer.parseInt(firstLine[1]);
        
        String[] secondLine = br.readLine().split(" ");
        Integer[] times = new Integer[N];
        for (int i = 0; i < N; i++) {
            times[i] = Integer.parseInt(secondLine[i]);
        }
        
        Arrays.sort(times, (a, b) -> b - a);
        
        PriorityQueue<Long> pq = new PriorityQueue<>();
        for (int i = 0; i < M; i++) {
            pq.offer(0L);
        }
        
        for (int time : times) {
            long minTime = pq.poll();
            pq.offer(minTime + time);
        }
        
        long result = 0;
        while (!pq.isEmpty()) {
            result = Math.max(result, pq.poll());
        }
        
        System.out.println(result);
    }
}
```
