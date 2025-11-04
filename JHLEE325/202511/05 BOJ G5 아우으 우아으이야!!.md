```java
import java.io.*;
import java.util.*;

public class Main {

    static class line implements Comparable<line> {
        int x, y;
        line(int x, int y) { this.x = x; this.y = y; }
        @Override
        public int compareTo(line o) {
            if (this.x != o.x) return Integer.compare(this.x, o.x);
            return Integer.compare(this.y, o.y);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());

        line[] arr = new line[N];
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            arr[i] = new line(a, b);
        }
        Arrays.sort(arr);

        long res = 0;
        int x = arr[0].x;
        int y = arr[0].y;

        for (int i = 1; i < N; i++) {
            int ns = arr[i].x;
            int ne = arr[i].y;
            if (ns <= y) {
                if (ne > y) {
                    y = ne;
                }
            } else {
                res += (long)(y - x);
                x = ns;
                y = ne;
            }
        }
        res += (long)(y - x);

        System.out.println(res);
    }
}
```
