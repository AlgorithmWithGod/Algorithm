```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] groups = {
            {0, 0}, {1, 2}, {3, 4}, {5, 6}, {7, 8}, {9, 10}, {11, 12}
    };
    private static int[] combination, firstInGroup;
    private static boolean[] visited;
    private static int[][] times;
    private static int minTime = Integer.MAX_VALUE;

    public static void main(String[] args) throws IOException {
        init();

        DFS(1);
        bw.write(minTime + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        times = new int[13][13];
        combination = new int[7];
        firstInGroup = new int[7];
        visited = new boolean[7];

        for (int i = 1; i <= 12; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= 12; j++) {
                times[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void DFS(int index) {
        if (index == 7) {
            for (int mask = 0; mask < (1 << 6); mask++) {
                for (int i = 1; i <= 6; i++) {
                    firstInGroup[i] = ((mask >> (i - 1)) & 1) == 0 ? 0 : 1;
                }
                int totalTime = cal();
                minTime = Math.min(minTime, totalTime);
            }
            return;
        }

        for (int i = 1; i <= 6; i++) {
            if (!visited[i]) {
                visited[i] = true;
                combination[index] = i;
                DFS(index + 1);
                visited[i] = false;
            }
        }
    }

    private static int cal() {
        int totalTime = 0;
        int prevStudent = -1;

        for (int i = 1; i <= 6; i++) {
            int index = combination[i];
            int[] group = groups[index];
            int first = group[firstInGroup[index]];
            int second = group[1 - firstInGroup[index]];

            if (i == 1) {
                totalTime += times[first][second];
                prevStudent = second;
            } else {
                totalTime += times[prevStudent][first];
                totalTime += times[first][second];
                prevStudent = second;
            }
        }

        return totalTime;
    }
}
```
