```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr, answer;
    private static int N, diff;
    public static void main(String[] args) throws IOException {
        init();
        solve();

        bw.write(answer[0] + " " + answer[1] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        answer = new int[2];
        diff = 2000000001;

        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);
    }

    private static void solve() {
        for (int i = 0; i < N-1; i++) {
            binarySearch(i);
        }
    }

    private static void binarySearch(int start) {
        int left = start+1;
        int right = N-1;

        while (left <= right) {
            int mid = left + (right-left)/2;
            int temp = arr[start]+arr[mid];


            if (temp < 0) {
                if (refresh(temp)) {
                    answer[0] = arr[start];
                    answer[1] = arr[mid];
                    diff = Math.abs(temp);
                }
                left = mid+1;
            } else if (temp == 0) {
                answer[0] = arr[start];
                answer[1] = arr[mid];
                diff = 0;
                return;
            } else {
                if (refresh(temp)) {
                    answer[0] = arr[start];
                    answer[1] = arr[mid];
                    diff = Math.abs(temp);
                }
                right = mid-1;
            }
        }
    }

    private static boolean refresh(int num) {
        return Math.abs(num) < diff;
    }
}
```
