```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr, combination, temp;
    private static int N, L, R, X, answer;

    public static void main(String[] args) throws IOException {
        init();
        for (int i = 2; i <= N; i++) {
            combination = new int[i];
            temp = new int[i];
            dfs(0, 0);
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        answer = 0;

        arr = new int[N];
        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

    }

    private static void dfs(int start, int index) {
        if (index == combination.length) {
            int[] clone = combination.clone();
            Arrays.sort(clone);
            int sum = Arrays.stream(clone).sum();
            if (sum < L) return;
            if (sum > R) return;
            if (clone[clone.length-1] - clone[0] < X) return;
            answer++;
            return;
        }

        for (int i = start; i < N; i++) {
            combination[index] = arr[i];
            temp[index] = i;
            dfs(i+1, index+1);
        }
    }
}

```
