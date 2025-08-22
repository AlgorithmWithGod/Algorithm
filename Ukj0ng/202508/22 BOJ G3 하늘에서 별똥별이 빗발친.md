```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] stars;
    private static int N, M, L, K, answer;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        answer = K;
        int max = 0;

        stars = new int[K][2];

        Set<Integer> xCandidates = new HashSet<>();
        Set<Integer> yCandidates = new HashSet<>();

        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());
            stars[i][0] = Integer.parseInt(st.nextToken());
            stars[i][1] = Integer.parseInt(st.nextToken());
            xCandidates.add(stars[i][0]);
            yCandidates.add(stars[i][1]);
        }

        for (int x : xCandidates) {
            for (int y : yCandidates) {
                int count = 0;

                for (int i = 0; i < K; i++) {
                    if (stars[i][0] >= x && stars[i][0] <= x + L &&
                            stars[i][1] >= y && stars[i][1] <= y + L) {
                        count++;
                    }
                }

                max = Math.max(max, count);
            }
        }

        answer -= max;
    }
}
```
