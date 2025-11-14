```java
import java.io.*;
import java.util.Arrays;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_19598_최소_회의실_개수 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int            N;
    private static Room[]         rooms;
    private static Queue<Integer> pq;

    private static class Room implements Comparable<Room> {

        int start;
        int end;

        Room(int start, int end) {
            this.start = start;
            this.end = end;
        }

        @Override
        public int compareTo(Room o) {
            if (this.start == o.start) {
                return Integer.compare(this.end, o.end);
            }
            return Integer.compare(this.start, o.start);
        }

        @Override
        public String toString() {
            return "[" + start + " " + end + "]";
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        rooms = new Room[N];
        pq = new PriorityQueue<>();
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());

            rooms[i] = new Room(s, e);
        }
        Arrays.sort(rooms);
        pq.offer(rooms[0].end);
    }

    private static void sol() throws IOException {
        for (int i = 1; i < N; i++) {
            if (rooms[i].start >= pq.peek()) {
                pq.poll();
            }
            pq.offer(rooms[i].end);
        }
        bw.write(pq.size() + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```