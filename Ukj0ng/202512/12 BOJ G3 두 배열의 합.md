```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] A, B;
    private static List<Long> sumA, sumB;
    private static int T, n, m;

    public static void main(String[] args) throws IOException {
        init();
        long answer = 0;

        for (int i = 0; i < sumA.size(); i++) {
            int left = lowerBound(sumA.get(i));
            int right = upperBound(sumA.get(i));

            answer += right-left;
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        T = Integer.parseInt(br.readLine());
        n = Integer.parseInt(br.readLine());
        A = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            A[i] = Integer.parseInt(st.nextToken());
        }

        m = Integer.parseInt(br.readLine());
        B = new int[m];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < m; i++) {
            B[i] = Integer.parseInt(st.nextToken());
        }

        sumA = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            long sum = 0;

            for (int j = i; j < n; j++) {
                sum += A[j];
                sumA.add(sum);
            }
        }

        sumB = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            long sum = 0;

            for (int j = i; j < m; j++) {
                sum += B[j];
                sumB.add(sum);
            }
        }

        sumB.sort((o1, o2) -> Long.compare(o1, o2));
    }

    private static int lowerBound(long a) {
        int left = 0;
        int right = sumB.size();

        while (left < right) {
            int mid = left + (right - left)/2;

            if (sumB.get(mid)+a >= T) {
                right = mid;
            } else {
                left = mid+1;
            }
        }

        return right;
    }

    private static int upperBound(long a) {
        int left = 0;
        int right = sumB.size();

        while (left < right) {
            int mid = left + (right - left)/2;

            if (sumB.get(mid)+a > T) {
                right = mid;
            } else {
                left = mid+1;
            }
        }

        return right;
    }
}
```
