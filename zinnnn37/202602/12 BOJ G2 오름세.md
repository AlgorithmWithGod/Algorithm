```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_3745_오름세 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int           N;
    private static String        line;
    private static int[]         stock;
    private static List<Integer> list;

    public static void main(String[] args) throws IOException {
        while ((line = br.readLine()) != null && !line.trim().isEmpty()) {
            init();
            sol();
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(line.trim());

        stock = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            stock[i] = Integer.parseInt(st.nextToken());
        }

        list = new ArrayList<>();
        list.add(0);
    }

    private static void sol() {
        for (int s : stock) {
            if (list.get(list.size() - 1) < s) {
                list.add(s);
            } else {
                int target = lowerBound(s);

                list.set(target, s);
            }
        }
        sb.append(list.size() - 1).append("\n");
    }

    private static int lowerBound(int target) {
        int left  = 0;
        int right = list.size() - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (list.get(mid) < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return right;
    }

}
```