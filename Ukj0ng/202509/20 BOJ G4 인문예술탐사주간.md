```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] trees;
    private static long[] prefix;
    private static int N, Q;

    public static void main(String[] args) throws IOException {
        init();

        while (Q-->0) {
            int X = Integer.parseInt(br.readLine());

            int pos = binarySearch(X);

            int a = pos;
            long A = prefix[pos];

            int b = N - pos;
            long B = prefix[N] - prefix[pos];

            long result = ((long) X * a - A) + (B - (long) X * b);
            bw.write(result + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        trees = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            trees[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(trees);

        prefix = new long[N+1];
        for (int i = 0; i < N; i++) {
            prefix[i+1] = prefix[i] + trees[i];
        }
    }

    private static int binarySearch(int n) {
        int start = 0;
        int end = N-1;

        while (start <= end) {
            int mid = start + (end-start)/2;

            if (trees[mid] <= n) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return start;
    }
}
```
