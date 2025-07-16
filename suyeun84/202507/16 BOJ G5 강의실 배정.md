```java
import java.util.*;
import java.io.*;

public class boj11000 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int answer = 0;
        PriorityQueue<Integer> rooms = new PriorityQueue<>();
        Time[] lec = new Time[N];
        for (int i = 0; i < N; i++) {
            nextLine();
            int S = nextInt();
            int T = nextInt();
            lec[i] = new Time(S, T);
        }
        Arrays.sort(lec, (o1, o2) -> {
            if (o1.s == o2.s) return o1.e - o2.e;
            else return o1.s - o2.s;
        });
        rooms.add(lec[0].e);
        for (int i = 1; i < N; i++) {
            if (rooms.peek() <= lec[i].s) rooms.poll();
            rooms.add(lec[i].e);
            answer = Math.max(answer, rooms.size());
        }
        System.out.println(answer);
    }
    static class Time {
        int s, e;
        public Time(int s, int e) {
            this.s = s;
            this.e = e;
        }
    }
}
```
