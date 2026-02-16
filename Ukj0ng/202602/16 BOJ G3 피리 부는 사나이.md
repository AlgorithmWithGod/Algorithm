```
import java.io.*;
import java.util.HashSet;
import java.util.Set;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Set<Integer> set;
    private static char[][] map;
    private static int[] uf, size;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                int x = i*M + j;
                int y = 0;
                int nx = i;
                int ny = j;
                if (map[i][j] == 'U') nx--;
                else if (map[i][j] == 'D') nx++;
                else if (map[i][j] == 'L') ny--;
                else ny++;

                y = nx*M + ny;
                int root1 = find(x);
                int root2 = find(y);

                if (root1 == root2) continue;
                union(root1, root2);
            }
        }

        for (int i = 0; i < N*M; i++) {
            set.add(find(i));
        }

        bw.write(set.size() + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new char[N][M];

        for (int i = 0; i < N; i++) {
            String input = br.readLine();
            for (int j = 0; j < M; j++) {
                map[i][j] = input.charAt(j);
            }
        }

        uf = new int[N*M];
        size = new int[N*M];

        for (int i = 0; i < N*M; i++) {
            uf[i] = i;
            size[i] = 1;
        }

        set = new HashSet<>();
    }

    private static void union(int x, int y) {
        if (size[x] < size[y]) {
            uf[x] = y;
            size[y] += size[x];
        } else {
            uf[y] = x;
            size[x] += size[y];
        }
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
