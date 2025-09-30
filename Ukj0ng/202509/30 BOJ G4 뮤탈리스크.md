```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {9, 9, 3, 3, 1, 1};
    private static final int[] dy = {3, 1, 9, 1, 3, 9};
    private static final int[] dz = {1, 3, 1, 9, 9, 3};
    private static Set<String> visited;
    private static int[] scv;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        scv = new int[3];
        visited = new HashSet<>();

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 3; i++) {
            if (N == i) break;
            scv[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = 0;
        visited.add(scv[0]+","+scv[1]+","+scv[2]);
        q.add(new int[]{scv[0], scv[1], scv[2], 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == 0 && current[1] == 0 && current[2] == 0) {
                result = current[3];
                break;
            }

            for (int i = 0; i < 6; i++) {
                int x = current[0] - dx[i] < 0 ? 0 : current[0] - dx[i];
                int y = current[1] - dy[i] < 0 ? 0 : current[1] - dy[i];
                int z = current[2] - dz[i] < 0 ? 0 : current[2] - dz[i];

                if (visited.contains(x+","+y+","+z)) continue;
                visited.add(x+","+y+","+z);
                q.add(new int[]{x, y, z, current[3]+1});
            }
        }

        return result;
    }
}
```
