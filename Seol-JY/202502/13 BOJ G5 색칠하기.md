```java

import java.io.*;
import java.util.*;
public class Main {
    private static final int EMPTY = 0;
    private static final int RED = 1;
    private static final int BLUE = -1;

    static int N, M;
    static int[][] arr;
    static int[] palette;
    static Queue<int[]> queue = new LinkedList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            N = nextInt(st);
            M = nextInt(st);
            arr = new int[N+1][N+1];
            palette = new int[N+1];
            
            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int x = nextInt(st);
                int y = nextInt(st);

                arr[x][y] = 1;
                arr[y][x] = 1;
            }
            boolean isImpossible = false;
            for (int i = 1; i < N+1; i++) { 
                if (palette[i] == EMPTY) {
                    if (!bfs(i)) {
                        System.out.println("impossible");
                        isImpossible = true;
                        break;
                    }
                }
            }
            if (!isImpossible) {
                System.out.println("possible");
            }
        }
    }

    private static boolean bfs(int i) {
        palette[i] = RED;
        queue.add(new int[]{i, RED});
        while (!queue.isEmpty()) {
            int[] target = queue.poll();

            for (int j = 1; j < N+1; j++) {
                if(arr[target[0]][j] == 1) {
                    if (palette[j] == target[1]) {
                        queue.clear();
                        return false;
                    }
                    if (palette[j] == EMPTY) {
                        palette[j] = -target[1];
                        queue.add(new int[]{j, -target[1]});
                    }
                }
            }
        }

        return true;
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
