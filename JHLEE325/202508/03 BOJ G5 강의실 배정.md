```java
import java.io.*;
import java.util.*;

public class Main {
    static class study implements Comparable<study> {
        int start, end;

        study(int s, int e) {
            start = s;
            end = e;
        }

        @Override
        public int compareTo(study o) {
            if (this.start != o.start)
                return Integer.compare(this.start, o.start);
            return Integer.compare(this.end, o.end);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        study[] studies = new study[N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            studies[i] = new study(s, e);
        }

        Arrays.sort(studies);

        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.add(studies[0].end);

        for (int i = 1; i < N; i++) {
            int curStart = studies[i].start;
            int curEnd = studies[i].end;
            if (!pq.isEmpty() && pq.peek() <= curStart) {
                pq.poll();
            }
            pq.add(curEnd);
        }

        System.out.println(pq.size());
    }
}
```
