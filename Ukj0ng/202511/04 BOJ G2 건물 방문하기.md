```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static TreeMap<Integer, List<Integer>> map;
    private static int N, H, W;
    public static void main(String[] args) throws IOException {
        init();
        int answer = greedy();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());
        W = Integer.parseInt(st.nextToken());

        map = new TreeMap<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            if (!map.containsKey(x)) map.put(x, new ArrayList<>());
            map.get(x).add(y);
        }

        for (int key : map.keySet()) {
            Collections.sort(map.get(key));
        }
    }

    private static int greedy() {
        int answer = 0;
        int[] start = new int[2];
        start[0] = 1;
        start[1] = 1;

        for (int floor : map.keySet()) {
            answer += (floor-start[0]) * 100;
            start[0] = floor;
            int leftDist = Math.abs(map.get(floor).get(0) - start[1]);
            int rightDist = Math.abs(map.get(floor).get(map.get(floor).size()-1) - start[1]);

            if (leftDist <= rightDist) {
                answer += (leftDist + map.get(floor).get(map.get(floor).size()-1) - map.get(floor).get(0));
                start[1] = map.get(floor).get(map.get(floor).size()-1);
            } else {
                answer += (rightDist + map.get(floor).get(map.get(floor).size()-1) - map.get(floor).get(0));
                start[1] = map.get(floor).get(0);
            }
        }

        return answer;
    }
}
```
