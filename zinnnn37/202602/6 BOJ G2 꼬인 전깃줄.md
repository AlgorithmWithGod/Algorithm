```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_1365_꼬인_전깃줄 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int           N;
    private static int[]         pairs;
    private static List<Integer> list;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        pairs = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            pairs[i] = Integer.parseInt(st.nextToken());
        }

        list = new ArrayList<>();
        list.add(0);
    }

    private static void sol() throws IOException {
        for (int pair : pairs) {
            int size = list.size();
            if (list.get(size - 1) < pair) {
                list.add(pair);
            } else {
                int target = lowerBound(pair, size);

                list.set(target, pair);
            }
        }
        int forward = N - list.size() + 1;

        bw.write(forward + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int lowerBound(int target, int right) {
        int left = 0;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (list.get(mid) >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return right;
    }

}
```