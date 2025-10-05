```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    static int N, M;
    static int[] parent;
    static List<int[]> parties = new ArrayList<>();

    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();

        parent = new int[N + 1];
        for (int i = 1; i <= N; i++) parent[i] = i;

        nextLine();
        int T = nextInt();
        int[] truth = new int[T];
        for (int i = 0; i < T; i++) truth[i] = nextInt();

        for (int i = 0; i < M; i++) {
            nextLine();
            int cnt = nextInt();
            int[] attendees = new int[cnt];
            for (int j = 0; j < cnt; j++) attendees[j] = nextInt();
            parties.add(attendees);

            for (int j = 1; j < cnt; j++) {
                union(attendees[0], attendees[j]);
            }
        }

        boolean[] truthRoot = new boolean[N + 1];
        for (int t : truth) {
            truthRoot[find(t)] = true;
        }

        int answer = 0;
        for (int[] party : parties) {
            boolean canLie = true;
            for (int p : party) {
                if (truthRoot[find(p)]) {
                    canLie = false;
                    break;
                }
            }
            if (canLie) answer++;
        }

        System.out.println(answer);
    }

    static int find(int x) {
        if (x == parent[x]) return x;
        return parent[x] = find(parent[x]);
    }

    static void union(int x, int y) {
        x = find(x);
        y = find(y);
        if (x == y) return;
        parent[y] = x;
    }
}
```
