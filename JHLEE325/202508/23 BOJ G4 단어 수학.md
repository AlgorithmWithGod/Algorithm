```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        int[] weight = new int[26];

        for (int i = 0; i < N; i++) {
            String word = br.readLine();
            int len = word.length();
            for (int j = 0; j < len; j++) {
                char c = word.charAt(j);
                weight[c - 'A'] += Math.pow(10, len - j - 1);
            }
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        for (int w : weight) {
            if (w > 0) pq.add(w);
        }

        int num = 9;
        int sum = 0;
        while (!pq.isEmpty()) {
            int val = pq.poll();
            sum += val * num--;
        }

        System.out.println(sum);
    }
}

```
