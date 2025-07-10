```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int M = nextInt();
        int L = nextInt();
        if (N > 0) nextLine();
        int[] pos = new int[N+2];
        pos[0] = 0;
        for (int i = 1; i <= N; i++) pos[i] = nextInt();
        pos[N+1] = L;
        Arrays.sort(pos);

        int start = 1, end = L-1;
        while (start <= end) {
            int mid = (start + end) / 2;
            int cnt = 0;
            for (int i = 1; i < N+2; i++) cnt += ((pos[i] - pos[i-1] - 1) / mid);

            if (cnt > M) start = mid + 1;
            else end = mid - 1;
        }
        System.out.println(start);
    }
}
```
