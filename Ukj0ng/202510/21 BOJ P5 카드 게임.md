```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] uf, cards;
    private static int N, M, K;
    public static void main(String[] args) throws IOException {
        init();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        cards = new int[M];
        uf = new int[M];

        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < M; i++) {
            cards[i] = Integer.parseInt(st.nextToken());
            uf[i] = i;
        }

        Arrays.sort(cards);

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < K; i++) {
            int input = Integer.parseInt(st.nextToken());
            int temp = binarySearch(input);
            int index = find(temp);

            bw.write(cards[index] + "\n");
            uf[index] = index + 1;
        }
    }

    private static int binarySearch(int target) {
        int left = 0;
        int right = M-1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (target < cards[mid]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
