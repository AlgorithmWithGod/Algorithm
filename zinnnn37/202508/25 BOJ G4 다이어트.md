```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class BJ_19942_다이어트 {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, mp, mf, ms, mv;
    private static int maxMask;
    private static int minCost;
    private static String bestResult;

    private static int[][] ingre;

    public static void main(String[] args) throws IOException {
        init();
        sol();
        printAns();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        st = new StringTokenizer(br.readLine());
        mp = Integer.parseInt(st.nextToken());
        mf = Integer.parseInt(st.nextToken());
        ms = Integer.parseInt(st.nextToken());
        mv = Integer.parseInt(st.nextToken());

        minCost = Integer.MAX_VALUE;
        bestResult = null;

        ingre = new int[N][5];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            ingre[i][0] = Integer.parseInt(st.nextToken()); // p
            ingre[i][1] = Integer.parseInt(st.nextToken()); // f
            ingre[i][2] = Integer.parseInt(st.nextToken()); // s
            ingre[i][3] = Integer.parseInt(st.nextToken()); // v
            ingre[i][4] = Integer.parseInt(st.nextToken()); // cost
        }
    }

    private static void sol() {
        maxMask = (1 << N);

        for (int mask = 1; mask < maxMask; mask++) {
            int sp = 0, sf = 0, ss = 0, sv = 0, sc = 0;
            StringBuilder sb = new StringBuilder();

            for (int i = 0, bit = 1; i < N; i++, bit <<= 1) {
                // 포함되는 재료
                if ((mask & bit) != 0) {
                    sp += ingre[i][0];
                    sf += ingre[i][1];
                    ss += ingre[i][2];
                    sv += ingre[i][3];
                    sc += ingre[i][4];
                    sb.append(i + 1).append(" ");
                }
            }

            if (sp >= mp && sf >= mf && ss >= ms && sv >= mv) {
                String currentResult = sb.toString();

                if (sc < minCost) {
                    minCost = sc;
                    bestResult = currentResult;
                } else if (sc == minCost) {
                    if (bestResult == null || currentResult.compareTo(bestResult) < 0) {
                        bestResult = currentResult;
                    }
                }
            }
        }
    }

    private static void printAns() throws IOException {
        if (bestResult == null) {
            bw.write("-1");
        } else {
            bw.write(minCost + "\n");
            bw.write(bestResult);
        }

        bw.flush();
        bw.close();
        br.close();
    }
}
```