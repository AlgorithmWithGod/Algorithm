```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr;
    private static int N, K;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            init();
            int answer = binarySearch();
            bw.write(answer + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);
    }

    private static int binarySearch() {
        int left = 0;
        int right = N-1;

        int minGap = (int)1e8 + 1;
        int count = 0;

        while (left < right) {
            int sum = arr[left] + arr[right];
            int gap = Math.abs(sum - K);

            if (gap < minGap) {
                minGap = gap;
                count = 1;
            } else if (gap == minGap) {
                count++;
            }

            if (sum < K) {
                left++;
            } else {
                right--;
            }
        }

        return count;
    }
}
```
