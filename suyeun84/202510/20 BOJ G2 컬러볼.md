```java
import java.io.*;
import java.util.*;

public class boj10800 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        Ball[] balls = new Ball[N];
        for (int i = 0; i < N; i++) {
            nextLine();
            balls[i] = new Ball(nextInt(), nextInt(), i);
        }
        // 공 색깔 별로
        Arrays.sort(balls, (o1, o2) -> o1.s - o2.s);
        int[] colors = new int[N+1];
        int[] answer = new int[N];
        int idx = 0, sum = 0;
        for (int i = 0; i < N; i++) {
            Ball curr = balls[i];
            while(balls[idx].s < curr.s) {
                sum += balls[idx].s;
                colors[balls[idx].c] += balls[idx].s;
                idx++;
            }
            answer[curr.idx] = sum - colors[curr.c];
        }
        for (int i = 0; i < N; i++) {
            System.out.println(answer[i]);
        }
    }

    static class Ball {
        int c, s, idx;
        public Ball(int c, int s, int idx) {
            this.c = c;
            this.s = s;
            this.idx = idx;
        }
    }
}
```
