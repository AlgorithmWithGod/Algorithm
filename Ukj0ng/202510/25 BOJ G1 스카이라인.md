```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static TreeMap<Integer, Integer> buildings;
    private static List<Event> events;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        int height = 0;
        for (Event event : events) {
            if (event.flag) {
                buildings.put(event.height, buildings.getOrDefault(event.height, 0)+1);
                if (height < buildings.lastKey()) {
                    height = buildings.lastKey();
                    bw.write(event.x + " " + height + " ");
                }
            } else {
                buildings.put(event.height, buildings.get(event.height)-1);
                if (buildings.get(event.height) == 0) buildings.remove(event.height);
                if (height > buildings.lastKey()) {
                    height = buildings.lastKey();
                    bw.write(event.x + " " + height + " ");
                }
            }
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        events = new ArrayList<>();
        buildings = new TreeMap<>();
        buildings.put(0, 1);

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int l = Integer.parseInt(st.nextToken());
            int h = Integer.parseInt(st.nextToken());
            int r = Integer.parseInt(st.nextToken());

            events.add(new Event(l, h, true));
            events.add(new Event(r, h, false));
        }

        events.sort((o1, o2) -> {
            if (o1.x != o2.x) return Integer.compare(o1.x, o2.x);
            
            if (o1.flag != o2.flag) {
                return o1.flag ? -1 : 1;
            } 
            
            if (o1.flag) {
                return Integer.compare(o2.height, o1.height);
            }
            return Integer.compare(o1.height, o2.height);
        });
    }

    static class Event {
        int x;
        int height;
        boolean flag;

        public Event(int x, int height, boolean flag) {
            this.x = x;
            this.height = height;
            this.flag = flag;
        }
    }
}
```
