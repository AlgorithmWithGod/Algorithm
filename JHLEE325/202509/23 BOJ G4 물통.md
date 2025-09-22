```java
import java.io.*;
import java.util.*;

public class Main {
    static int afull, bfull, cfull;
    static boolean[][][] visited;
    static boolean[] possible;

    static class State {
        int a, b, c;
        State(int a, int b, int c) {
            this.a = a;
            this.b = b;
            this.c = c;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        afull = Integer.parseInt(st.nextToken());
        bfull = Integer.parseInt(st.nextToken());
        cfull = Integer.parseInt(st.nextToken());

        visited = new boolean[afull + 1][bfull + 1][cfull + 1];
        possible = new boolean[cfull + 1];

        bfs();

        StringBuilder sb = new StringBuilder();
        for(int i=0;i<possible.length;i++){
            if(possible[i])
                sb.append(i+" ");
        }
        System.out.println(sb.toString().trim());
    }

    static void bfs() {
        Queue<State> q = new LinkedList<>();

        q.offer(new State(0, 0, cfull));
        visited[0][0][cfull] = true;

        while (!q.isEmpty()) {
            State cur = q.poll();
            int a = cur.a, b = cur.b, c = cur.c;

            if (a == 0) {
                possible[c]=true;
            }

            move(a, b, c, 0, 1, q);
            move(a, b, c, 0, 2, q);
            move(a, b, c, 1, 0, q);
            move(a, b, c, 1, 2, q);
            move(a, b, c, 2, 0, q);
            move(a, b, c, 2, 1, q);
        }
    }

    static void move(int a, int b, int c, int from, int to, Queue<State> q) {
        int[] cur = new int[]{a, b, c};
        int[] cap = new int[]{afull, bfull, cfull};

        if (cur[from] == 0) return;

        int movewater = Math.min(cur[from], cap[to] - cur[to]);
        cur[from] -= movewater;
        cur[to] += movewater;

        int na = cur[0], nb = cur[1], nc = cur[2];
        if (!visited[na][nb][nc]) {
            visited[na][nb][nc] = true;
            q.offer(new State(na, nb, nc));
        }
    }
}
```
