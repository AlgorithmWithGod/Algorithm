```java
import java.io.*;
import java.util.*;

public class Main {

    static class homework implements Comparable<homework> {
        int deadline;
        int score;
        homework(int d, int s) {
            deadline = d;
            score = s;
        }
        @Override
        public int compareTo(homework o){
            return this.deadline - o.deadline;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        homework[] hw = new homework[N];
        int duedate = 0;

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int d = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            hw[i] = new homework(d, w);
            if (d > duedate) duedate = d;
        }

        Arrays.sort(hw);

        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        long result = 0;
        int idx = N - 1;

        for (int day = duedate; day >= 1; day--) {
            while (idx >= 0 && hw[idx].deadline >= day) {
                pq.offer(hw[idx].score);
                idx--;
            }

            if (!pq.isEmpty()) {
                result += pq.poll();
            }
        }

        System.out.println(result);
    }
}
```
