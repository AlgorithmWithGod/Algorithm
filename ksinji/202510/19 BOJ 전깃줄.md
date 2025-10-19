```java
import java.io.*;
import java.util.*;

public class Main {
    static class Wire implements Comparable<Wire> {
        int a, b;
        Wire(int a, int b) { 
            this.a = a; 
            this.b = b; 
        }

        @Override
        public int compareTo(Wire o) {
            return this.a - o.a;
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        Wire[] arr = new Wire[N];
        int[] dp = new int[N];
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            arr[i] = new Wire(a, b);
        }

        Arrays.sort(arr);

        int max = 1;
        for (int i = 0; i < N; i++) {
            dp[i] = 1;
            for (int j = 0; j < i; j++) {
                if (arr[i].b > arr[j].b) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            max = Math.max(max, dp[i]);
        }
```
        System.out.println(N - max);
    }
}
