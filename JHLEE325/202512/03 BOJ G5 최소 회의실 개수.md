```java
import java.io.*;
import java.util.*;

public class Main {

    static class Meeting {
        int s, e;
        Meeting(int s, int e) {
            this.s = s;
            this.e = e;
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        Meeting[] arr = new Meeting[N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            arr[i] = new Meeting(s, e);
        }

        // 시작 시간 기준 정렬
        Arrays.sort(arr, (a, b) -> a.s - b.s);

        // 종료 시간을 저장하는 최소 힙
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < N; i++) {
            int start = arr[i].s;
            int end   = arr[i].e;

            // 이미 끝난 회의는 회의실 재사용
            if (!pq.isEmpty() && pq.peek() <= start) {
                pq.poll();
            }

            pq.offer(end);
        }

        System.out.println(pq.size());
    }
}
```
