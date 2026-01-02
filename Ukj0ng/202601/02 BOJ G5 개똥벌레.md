```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] bottom, top;
    private static int N, H;

    public static void main(String[] args) throws IOException {
        init();
        int count = 0;
        int answer = 20000001;

        for (int i = 1; i <= H; i++) {
            int t = topBinarySearch(i);
            int b = bottomBinarySearch(i);

            if (t+b < answer) {
                answer = t+b;
                count = 1;
            } else if (t+b == answer) {
                count++;
            }
        }

        bw.write(answer + " " + count + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        bottom = new int[N/2];
        top = new int[N/2];

        for (int i = 0; i < N/2; i++) {
            bottom[i] = Integer.parseInt(br.readLine());
            top[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(bottom);
        Arrays.sort(top);
    }

    private static int bottomBinarySearch(int h) {
        int left = 0;
        int right = N/2-1;
        int result = -1;

        while (left <= right) {
            int mid = left+(right-left)/2;

            if (bottom[mid] >= h) {
                result = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }

        return result == -1 ? 0 : N/2-result;
    }

    private static int topBinarySearch(int h) {
        int left = 0;
        int right = N/2-1;
        int result = -1;

        while (left <= right) {
            int mid = left+(right-left)/2;

            if (top[mid] >= H-h+1) {
                result = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }

        return result == -1 ? 0 : N/2-result;
    }
}
```
