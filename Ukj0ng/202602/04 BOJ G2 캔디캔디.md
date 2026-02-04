```
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long)Math.pow(2, 64);
    private static long[] arr;
    private static long sum, answer;
    private static int M, N;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());

        arr = new long[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Long.parseLong(br.readLine());
            sum += arr[i];
        }

        Arrays.sort(arr);

        long temp = sum - M;

        for (int i = 0; i < N; i++) {
            long n = temp / (N-i);
            if (n >= arr[i]) {
                temp -= arr[i];
                answer = (arr[i]*arr[i] + answer) % INF;
            } else {
                temp -= n;
                answer = (n*n + answer) % INF;
            }
        }
    }
}
```
