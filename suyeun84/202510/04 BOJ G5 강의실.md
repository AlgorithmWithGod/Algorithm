```java
import java.io.*;
import java.util.*;

public class boj1374 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        Lecture[] arr = new Lecture[n];
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            st.nextToken();
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            arr[i] = new Lecture(start, end);
        }
        Arrays.sort(arr, (o1, o2) -> o1.start - o2.start);
        PriorityQueue<Lecture> pq = new PriorityQueue<>();
        pq.add(arr[0]);
        for (int i = 1; i < n; i++) {
            Lecture current = pq.peek();
            if (current.end <= arr[i].start) {
                pq.poll();
                current.end = arr[i].end;
                pq.add(current);
            } else {
                pq.add(arr[i]);
            }

        }
        System.out.println(pq.size());

    }


    public static class Lecture implements Comparable<Lecture> {
        int start;
        int end;

        public Lecture(int start, int end) {
            this.start = start;
            this.end = end;
        }

        @Override
        public int compareTo(Lecture o) {
            if (this.end == o.end) return this.start - o.start;
            return this.end - o.end;
        }
    }
}
```
