```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.StringTokenizer;

public class Main {
    private static int N;
    private static int[][] map;
    private static int[] burn;
    private static int[] mark;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = nextInt(st);
        map = new int[N+1][N+1];
        burn = new int[N+1];
        mark = new int[N+1];

        int M = nextInt(st);

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int x = nextInt(st);
            int y = nextInt(st);

            map[x][y] = 1;
            map[y][x] = 1;
        }

        int T = Integer.parseInt(br.readLine());
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < T; i++) {
            int value = nextInt(st);
            burn[value] = 1;
            mark[value] = 1;
        }

        List<Integer> answers = new ArrayList<>();
        for (int i = 1; i <= N; i++) {
            if (burn[i] == 1) {
                if (extinguish(i)) {
                    answers.add(i);
                }
            } 
        }
    
        if (Arrays.stream(mark).sum() == 0) {
            System.out.println(answers.size());
            for (Integer a : answers) {
                System.out.print(a + " ");
            }

            return;
        }

        System.out.println(-1);
    }

    private static boolean extinguish(int value) {
        for (int i = 1; i < N+1; i++) {
            if (i == value) continue;
            if (map[value][i] == 1 && burn[i] != 1) {
                return false;
            }
        }
        mark[value] = 0;
        for (int i =1; i < N+1; i++) {
            if (map[value][i] == 1) {
                mark[i] = 0;
            }
        }

        return true;
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
