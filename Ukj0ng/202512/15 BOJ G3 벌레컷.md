```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr;
    private static long[] sum;
    private static int N;
    private static long answer;

    public static void main(String[] args) throws IOException {
        init();
        for (int i = 0; i < N-1; i++) {
            int max = upperBound(i);
            int min = lowerBound(i);

            if (max != -1 && min != -1 && min <= max) {
                answer += (max-min+1);
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        sum = new long[N];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            if (i == 0) sum[i] = arr[i];
            else sum[i] = sum[i-1]+arr[i];
        }
    }

    private static int upperBound(int head) {
        int left = head+1;
        int right = N-2;
        int result = -1;

        while (left <= right) {
            int mid = left + (right-left)/2;

            if (sum[head] < (sum[N-1]-sum[mid])) {
                result = mid;
                left = mid+1;
            } else {
                right = mid-1;
            }
        }
        return result;
    }

    private static int lowerBound(int head) {
        int left = head+1;
        int right = N-2;
        int result = -1;

        while (left <= right) {
            int mid = left + (right-left)/2;

            if ((sum[N-1]-sum[mid]) < (sum[mid]-sum[head])) {
                result = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }
        return result;
    }
}
```
