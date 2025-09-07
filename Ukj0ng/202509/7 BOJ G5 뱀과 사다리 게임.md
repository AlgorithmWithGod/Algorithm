```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] board;
    private static boolean[] visited;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        board = new int[101];
        visited = new boolean[101];

        for (int i = 0; i < N+M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            board[a] = b;
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = 0;
        visited[1] = true;
        q.add(new int[] {1, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == 100) {
                result = current[1];
                break;
            }

            for (int i = 1; i <= 6; i++) {
                int next = current[0] + i;
                if (next > 100) continue;

                if (board[next] != 0) {
                    next = board[next];
                }

                if (visited[next]) continue;
                visited[next] = true;
                q.add(new int[]{next, current[1] + 1});
            }
        }

        return result;
    }
}
```
