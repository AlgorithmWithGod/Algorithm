```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static class Lecture {
        int start;
        int end;

        public Lecture(int start, int end) {
            this.start = start;
            this.end = end;
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        Lecture[] lectures = new Lecture[N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            Lecture lecture =  new Lecture(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
            lectures[i] = lecture;
        }

        // 시작 시간 기준 오름차순 강의 정렬
        Arrays.sort(lectures, new Comparator<Lecture>() {
            @Override
            public int compare(Lecture o1, Lecture o2) {
                return Integer.compare(o1.start, o2.start);
            }
        });

        // 끝나는 시간 기준 오름차순 우선순위 큐
        PriorityQueue<Lecture> pq = new PriorityQueue<>(new Comparator<Lecture>() {
            @Override
            public int compare(Lecture o1, Lecture o2) {
                return Integer.compare(o1.end, o2.end);
            }
        });

        for (Lecture current : lectures) {
            if (!pq.isEmpty() && pq.peek().end <= current.start) {
                pq.poll(); // 기존 강의실
            }
            pq.offer(current);
        }
        System.out.println(pq.size());
        br.close();
    }
}
```
