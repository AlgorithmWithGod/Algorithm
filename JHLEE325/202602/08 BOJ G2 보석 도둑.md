```java
import java.io.*;
import java.util.*;

class Diamond implements Comparable<Diamond> {
    int weight, value;

    public Diamond(int weight, int value) {
        this.weight = weight;
        this.value = value;
    }

    @Override
    public int compareTo(Diamond o) {
        return this.weight - o.weight;
    }
}

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        Diamond[] dia = new Diamond[N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int m = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            dia[i] = new Diamond(m, v);
        }

        int[] bags = new int[K];
        for (int i = 0; i < K; i++) {
            bags[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(dia);
        Arrays.sort(bags);

        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        long totalPrice = 0;
        int diaIdx = 0;

        for (int i = 0; i < K; i++) {
            while (diaIdx < N && dia[diaIdx].weight <= bags[i]) {
                pq.add(dia[diaIdx].value);
                diaIdx++;
            }

            if (!pq.isEmpty()) {
                totalPrice += pq.poll();
            }
        }

        System.out.println(totalPrice);
    }
}
```
