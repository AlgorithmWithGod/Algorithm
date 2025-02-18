```java
import java.util.*;
import java.io.*;

public class Main {
    static int N;
    static int[][] arr;
    static int[][] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = nextInt(st);
        int M = nextInt(st);

        arr = new int[N][N];
        visited = new int[N][N];
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            arr[nextInt(st) - 1][nextInt(st) - 1] = 1;
        }

        for (int i = 0; i < N; i++) {
            bfs(i);
        }

        int answer = 0;
        for (int i = 0; i < N; i++) {
            boolean good = true;
            for (int j = 0; j < N; j++) {
                if (i  == j) continue;
                if(visited[i][j] + visited[j][i] < 1) {
                    good = false;
                }
            }
            if (good) {
                answer++;
            }
        }

        System.out.println(answer);
    }

    private static void bfs(int start) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(start);

        while (!queue.isEmpty()) {
            int target = queue.poll();

            for (int i = 0; i < N; i++) {
                if (arr[target][i] == 1 && visited[start][i] != 1) {
                    visited[start][i] = 1;
                    queue.add(i);
                }
            }
        }
        
    }

    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
