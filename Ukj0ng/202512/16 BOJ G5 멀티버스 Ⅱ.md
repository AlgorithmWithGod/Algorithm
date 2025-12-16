```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] arr, sortedArr, ranks;
    private static int M, N, answer;

    public static void main(String[] args) throws IOException {
        init();
        for (int i = 0; i < M-1; i++) {
            for (int j = i+1; j < M; j++) {
                boolean same = true;
                for (int k = 0; k < N; k++) {
                    if (ranks[i][k] != ranks[j][k]) {
                        same = false;
                        break;
                    }
                }

                if (same) answer++;
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());

        arr = new int[M][N];
        ranks = new int[M][N];
        sortedArr = new int[M][];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            Set<Integer> set = new HashSet<>();
            for (int j = 0; j < N; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                set.add(arr[i][j]);
            }

            sortedArr[i] = new int[set.size()];
            int index = 0;
            for (Integer e : set) {
                sortedArr[i][index++] = e;
            }
            Arrays.sort(sortedArr[i]);
        }

        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                ranks[i][j] = binarySearch(i, arr[i][j]);
            }
        }
    }

    private static int binarySearch(int index, int val) {
        int left = 0;
        int right = sortedArr[index].length-1;
        int result = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (val == sortedArr[index][mid]) {
                result = mid;
                break;
            } else if (val > sortedArr[index][mid]) {
                left = mid+1;
            } else {
                right = mid-1;
            }
        }

        return result;
    }
}
```
