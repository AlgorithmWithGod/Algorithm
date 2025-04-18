```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> {
            if (a[1] == b[1]) {
                return a[0] - b[0];
            } else {
                return a[1] - b[1];
            }
        });
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            pq.add(new int[] {Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())});
        }
        int cnt = 0;
        int curTime = 0;
        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            if (cur[0] >= curTime) {
                cnt++;
                curTime = cur[1];
            }
        }
        bw.write(cnt + "");
        bw.close();
    }
}



```
