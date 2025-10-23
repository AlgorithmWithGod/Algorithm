```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Event> events;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        int answer = sweep();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        events = new ArrayList<>();

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());

            double angle1 = Math.atan2(y1, x1);
            double angle2 = Math.atan2(y2, x2);

            if (angle1 > angle2) {
                double temp = angle1;
                angle1 = angle2;
                angle2 = temp;
            }

            events.add(new Event(angle1, i, true));
            events.add(new Event(angle2, i, false));
        }

        events.sort((o1, o2) -> {
            if (o1.angle == o2.angle) {
                if (o1.start != o2.start) return o1.start ? -1 : 1;
                return 0;
            }

            return Double.compare(o1.angle, o2.angle);
        });
    }

    private static int sweep() {
        int result = 0;
        int count = 0;

        for (Event event : events) {
            if (event.start) {
                count++;
                result = Math.max(result, count);
            } else {
                count--;
            }
        }

        return result;
    }

    static class Event {
        double angle;
        int index;
        boolean start;

        public Event(double angle, int index, boolean start) {
            this.angle = angle;
            this.index = index;
            this.start = start;
        }
    }
}
```
