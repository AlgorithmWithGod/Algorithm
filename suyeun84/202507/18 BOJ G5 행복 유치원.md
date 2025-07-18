```java
import java.util.*;
import java.io.*;

public class boj13164 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        int N, K, answer = 0;
        nextLine();
        N = nextInt();
        K = nextInt();
        nextLine();
        int[] h = new int[N];
        for (int i = 0; i < N; i++) h[i] = nextInt();

        int[] diff = new int[N - 1];
        for (int i = 0; i < N - 1; i++) diff[i] = h[i + 1] - h[i];

        Arrays.sort(diff);
        for (int i = 0; i < N - K; i++) answer += diff[i];
        System.out.println(answer);
    }
}
```
