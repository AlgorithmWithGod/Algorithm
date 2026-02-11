```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_16566_카드_게임 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, M, K;
    private static int[] cards, choices, parents;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        cards = new int[M];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            cards[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(cards);

        choices = new int[K];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < K; i++) {
            choices[i] = Integer.parseInt(st.nextToken());
        }

        parents = new int[M + 1];
        for (int i = 0; i < M; i++) {
            parents[i] = i;
        }
    }

    private static void sol() throws IOException {
        for (int i = 0; i < K; i++) {
            int target = find(upperBound(choices[i]));
            sb.append(cards[parents[target]]).append("\n");

            union(target, target + 1);
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static int upperBound(int choice) {
        int left  = 0;
        int right = M - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (cards[mid] <= choice) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return right;
    }

    private static int find(int a) {
        if (parents[a] == a) {
            return a;
        }

        return parents[a] = find(parents[a]);
    }

    private static void union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);

        parents[rootA] = rootB;
    }

}
```