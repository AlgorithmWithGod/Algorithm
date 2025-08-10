```java
import java.io.*;
import java.util.*;

public class Main {

    static boolean[] broken = new boolean[10];

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine().trim());
        int m = Integer.parseInt(br.readLine().trim());

        if (m > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 0; i < m; i++) {
                broken[Integer.parseInt(st.nextToken())] = true;
            }
        }

        int answer = Math.abs(n - 100);

        for (int ch = 0; ch <= 1000000; ch++) {
            int len = canpress(ch);
            if (len == -1) continue;
            int press = len + Math.abs(n - ch);
            if (press < answer) answer = press;
        }

        System.out.println(answer);
    }

    static int canpress(int ch) {
        if (ch == 0) return broken[0] ? -1 : 1;
        int len = 0;
        while (ch > 0) {
            int d = ch % 10;
            if (broken[d]) return -1;
            len++;
            ch /= 10;
        }
        return len;
    }
}

```
