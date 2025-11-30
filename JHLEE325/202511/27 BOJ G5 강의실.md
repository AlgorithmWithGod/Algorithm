```java
import java.io.*;
import java.util.*;

public class Main {

    static class study {
        int s, e;
        study(int s, int e) {
            this.s = s;
            this.e = e;
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        study[] arr = new study[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            st.nextToken();
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            arr[i] = new study(s, e);
        }

        Arrays.sort(arr, (a, b) -> a.s - b.s);

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (study s : arr) {
            if (!pq.isEmpty() && pq.peek() <= s.s) {
                pq.poll();
            }

            pq.offer(s.e);
        }

        System.out.println(pq.size());
    }
}
```
