```
import java.io.*;
import java.util.ArrayDeque;
import java.util.HashSet;
import java.util.Queue;
import java.util.Set;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Set<String> visited;
    private static int S;
    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        S = Integer.parseInt(br.readLine());
        visited = new HashSet<>();
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int time = 0;
        visited.add(1+","+0);
        // 이모티콘 개수, 클립보드 개수, 시간
        q.add(new int[]{1, 0, time});

        while (!q.isEmpty()) {
            int[] current = q.poll();
            if (current[0] == S) {
                time = current[2];
                break;
            }

            for (int i = 0; i < 3; i++) {
                if (i == 0) {
                    q.add(new int[]{current[0], current[0], current[2]+1});
                } else if (i == 1 && current[1] > 0) {
                    if (visited.contains(current[0]+current[1] + "," + current[1])) continue;
                    visited.add(current[0]+current[1] + "," + current[1]);
                    q.add(new int[]{current[0]+current[1], current[1], current[2]+1});
                } else {
                    if (current[0]-1<0 || visited.contains(current[0]-1 + "," + current[1])) continue;
                    visited.add(current[0]-1 + "," + current[1]);
                    q.add(new int[]{current[0]-1, current[1], current[2]+1});
                }
            }
        }

        return time;
    }
}
```
