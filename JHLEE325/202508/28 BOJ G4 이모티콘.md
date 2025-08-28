```java
import java.io.*;
import java.util.*;

public class Main {

    static class State {
        int cur, clip;

        State(int cur, int clip) {
            this.cur = cur;
            this.clip = clip;
        }
    }

    static int s;
    static int range = 2000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        s = Integer.parseInt(br.readLine());
        System.out.println(bfs());
    }

    static int bfs() {
        int[][] dist = new int[range + 1][range + 1];
        for (int i = 0; i <= range; i++) Arrays.fill(dist[i], -1);

        ArrayDeque<State> q = new ArrayDeque<>();
        q.add(new State(1, 0));
        dist[1][0] = 0;

        while (!q.isEmpty()) {
            State now = q.poll();
            int cur = now.cur;
            int clip = now.clip;
            int t = dist[cur][clip];

            if (cur == s)
                return t;

            if (dist[cur][cur] == -1) {
                dist[cur][cur] = t + 1;
                q.add(new State(cur, cur));
            }

            if (clip > 0 && cur + clip <= range && dist[cur + clip][clip] == -1) {
                dist[cur + clip][clip] = t + 1;
                q.add(new State(cur + clip, clip));
            }

            if (cur > 0 && dist[cur - 1][clip] == -1) {
                dist[cur - 1][clip] = t + 1;
                q.add(new State(cur - 1, clip));
            }
        }
        return -1;
    }
}

```
