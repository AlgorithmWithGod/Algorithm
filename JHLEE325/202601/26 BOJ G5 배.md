```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        Integer[] cranes = new Integer[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            cranes[i] = Integer.parseInt(st.nextToken());
        }

        int m = Integer.parseInt(br.readLine());
        List<Integer> boxes = new ArrayList<>();

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < m; i++) boxes.add(Integer.parseInt(st.nextToken()));

        Arrays.sort(cranes, Collections.reverseOrder());
        Collections.sort(boxes, Collections.reverseOrder());

        if (boxes.get(0) > cranes[0]) {
            System.out.println("-1");
            return;
        }

        int time = 0;
        while (!boxes.isEmpty()) {
            int boxIdx = 0;
            for (int i = 0; i < n; ) {
                if (boxIdx == boxes.size()) break;

                if (cranes[i] >= boxes.get(boxIdx)) {
                    boxes.remove(boxIdx);
                    i++;
                } else {
                    boxIdx++;
                }
            }
            time++;
        }

        System.out.println(time);
    }
}
```
