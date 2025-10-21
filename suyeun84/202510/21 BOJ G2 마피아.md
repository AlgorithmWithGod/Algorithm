```java
import java.io.*;
import java.util.*;

public class boj1079 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    static boolean[] isDead;
    static int N, mafia, answer = 0;
    static int[][] R;
    static int[] guilty;
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        isDead = new boolean[N];
        guilty = new int[N];
        mafia = -1;
        R = new int[N][N];
        nextLine();
        for (int i = 0; i < N; i++) guilty[i] = nextInt();
        for (int i = 0; i < N; i++) {
            nextLine();
            for (int j = 0; j < N; j++) {
                R[i][j] = nextInt();
            }
        }
        nextLine();
        mafia = nextInt();
        dfs(N, 0);

        System.out.println(answer);
    }

    static void dfs(int alive, int nights) {
        if (isDead[mafia] || alive == 1) {
            answer = Math.max(answer, nights);
            return;
        }
        if (alive % 2 == 0) { // 밤
            for (int i = 0; i < N; i++) {
                if (isDead[i] || i == mafia) continue;
                isDead[i] = true;
                changeGuilty(1, i);
                dfs(alive-1, nights+1);
                changeGuilty(-1, i);
                isDead[i] = false;
            }
        } else { // 낮
            int maxGuilty = Integer.MIN_VALUE;
            int idx = -1;
            for (int i = 0; i < N; i++) {
                if (isDead[i] || guilty[i] <= maxGuilty) continue;
                maxGuilty = guilty[i];
                idx = i;
            }
            isDead[idx] = true;
            dfs(alive-1, nights);
            isDead[idx] = false;
        }
    }

    static void changeGuilty(int type, int idx) {
        for (int i = 0; i < N; i++) {
            if (isDead[i]) continue;
            guilty[i] += type * R[idx][i];
        }
    }
 }
```
