```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] piles, flagpole;
    private static double answer;
    private static int N, M, R;

    public static void main(String[] args) throws IOException {
        init();

        for (int i = 0; i < N-1; i++) {
            for (int j = i+1; j < N; j++) {
                checkTriangle(i, j);
            }
        }

        if (answer < 0) {
            bw.write("-1\n");
        } else {
            bw.write(String.format("%.1f\n", answer));
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        answer = -1;

        piles = new int[N];
        flagpole = new int[M];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            piles[i] = Integer.parseInt(st.nextToken()) + 20000;
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            flagpole[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(piles);
        Arrays.sort(flagpole);
    }

    private static void checkTriangle(int i, int j) {
        int width = piles[j] - piles[i];
        
        double maxHeight = 2.0 * R / width;

        int left = 0, right = M - 1;
        int bestIdx = -1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (flagpole[mid] <= maxHeight) {
                bestIdx = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        if (bestIdx >= 0) {
            double area = (double)width * flagpole[bestIdx] / 2.0;
            answer = Math.max(answer, area);
        }
    }
}
```
