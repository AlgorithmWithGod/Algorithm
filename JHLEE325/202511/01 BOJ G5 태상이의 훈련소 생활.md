```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        long[] h = new long[N + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) h[i] = Long.parseLong(st.nextToken());

        long[] diff = new long[N + 3];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            long k = Long.parseLong(st.nextToken());
            diff[a] += k;
            diff[b + 1] -= k;
        }

        StringBuilder sb = new StringBuilder();
        long acc = 0;
        for (int i = 1; i <= N; i++) {
            acc += diff[i];
            sb.append(h[i] + acc).append(' ');
        }

        System.out.println(sb.toString().trim());
    }
}
```
