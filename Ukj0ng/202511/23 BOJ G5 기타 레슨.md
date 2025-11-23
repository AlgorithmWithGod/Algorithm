```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] lectures;
    private static int N, M, min;

    public static void main(String[] args) throws IOException {
        init();
        int answer = binarySearch();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        min = 10000;

        lectures = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            lectures[i] = Integer.parseInt(st.nextToken());
            min = Math.min(min, lectures[i]);
        }
    }

    private static int binarySearch() {
        int left = min;
        int right = 1000000000;
        int result = 0;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (valid(mid)) {
                result = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return result;
    }

    private static boolean valid(int target) {
        int time = 0;
        int count = 1;

        for (int lecture : lectures) {
            if (lecture > target) {
                return false;
            }
            if (time + lecture <= target) {
                time += lecture;
            } else {
                count++;
                time = lecture;
            }
        }

        return count <= M;
    }
}
```
