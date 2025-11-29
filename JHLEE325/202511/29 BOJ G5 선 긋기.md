```java
import java.io.*;
import java.util.*;

public class Main {

    static class line {
        int x, y;
        line(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        line[] arr = new line[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            if (a > b) {
                int temp = a;
                a = b;
                b = temp;
            }

            arr[i] = new line(a, b);
        }

        Arrays.sort(arr, (o1, o2) -> {
            if (o1.x == o2.x) return o1.y - o2.y;
            return o1.x - o2.x;
        });

        long answer = 0;

        int curStart = arr[0].x;
        int curEnd = arr[0].y;

        for (int i = 1; i < N; i++) {
            int nx = arr[i].x;
            int ny = arr[i].y;

            if (nx <= curEnd) {
                curEnd = Math.max(curEnd, ny);
            } else {
                answer += (curEnd - curStart);
                curStart = nx;
                curEnd = ny;
            }
        }

        answer += (curEnd - curStart);

        System.out.println(answer);
    }
}
```
