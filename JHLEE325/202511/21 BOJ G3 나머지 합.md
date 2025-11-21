```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        long[] count = new long[M];
        long answer = 0;

        long prefix = 0;

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            prefix = (prefix + Integer.parseInt(st.nextToken())) % M;
            count[(int) prefix]++;
        }

        answer += count[0];

        for (int i = 0; i < M; i++) {
            long c = count[i];
            if (c >= 2) {
                answer += (c * (c - 1)) / 2;
            }
        }

        System.out.println(answer);
    }
}
```
