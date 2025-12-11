```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] arr;
    private static int[] memo;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        int maxLen = DP();

        bw.write((N-maxLen) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        arr = new int[N][2];
        memo = new int[N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            arr[i][0] = a;
            arr[i][1] = b;
        }

        Arrays.sort(arr, (o1, o2) -> Integer.compare(o1[0], o2[0]));
    }

    private static int DP() {
        int len = 0;

        for (int i = 0; i < N; i++) {
            int key = arr[i][1];

            if (len == 0 || memo[len - 1] < key) {
                memo[len] = key;
                len++;
            } else {
                int index = binarySearch(len - 1, key);
                memo[index] = key;
            }
        }

        return len;
    }

    private static int binarySearch(int right, int key) {
        int left = 0;

        while (left < right) {
            int mid = left + (right-left)/2;

            if (memo[mid] >= key) {
                right = mid;
            }
            else left = mid+1;
        }

        return right;
    }
}
```
