```
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr, lis;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        int answer = DP();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        StringTokenizer st = new StringTokenizer(br.readLine());
        arr = new int[N];
        lis = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static int DP() {
        int len = 0;

        for (int i = 0; i < N; i++) {
            int key = arr[i];

            if (len == 0 || lis[len-1] < key) {
                lis[len] = key;
                len++;
            } else {
                int index = binarySearch(len-1, key);
                lis[index] = key;
            }
        }

        return len;
    }

    private static int binarySearch(int right, int key) {
        int left = 0;

        while (left < right) {
            int mid = left + (right-left)/2;

            if (lis[mid] >= key) {
                right = mid;
            } else {
                left = mid+1;
            }
        }

        return right;
    }
}
```
