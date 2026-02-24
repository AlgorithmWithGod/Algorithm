```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        while (T-- > 0) {
            int M = Integer.parseInt(br.readLine());
            sb.append((M + 1) / 2).append("\n");

            PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();

            int count = 0;
            StringTokenizer st = null;

            for (int i = 0; i < M; i++) {
                if (i % 10 == 0) {
                    st = new StringTokenizer(br.readLine());
                }

                int num = Integer.parseInt(st.nextToken());

                if (maxHeap.size() == minHeap.size()) maxHeap.add(num);
                else minHeap.add(num);

                if (!minHeap.isEmpty() && maxHeap.peek() > minHeap.peek()) {
                    int tmp1 = maxHeap.poll();
                    int tmp2 = minHeap.poll();
                    maxHeap.add(tmp2);
                    minHeap.add(tmp1);
                }

                if (i % 2 == 0) {
                    sb.append(maxHeap.peek()).append(" ");
                    count++;
                    if (count % 10 == 0) sb.append("\n");
                }
            }
            if (count % 10 != 0) sb.append("\n");
        }
        System.out.print(sb.toString());
    }
}
```
