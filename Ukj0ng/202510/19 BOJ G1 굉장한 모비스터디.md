```
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<Integer, Set<Integer>> map;
    private static List<List<Integer>> temp;
    private static int[][] uf, size;
    private static int N, M1, M2, M3;

    public static void main(String[] args) throws IOException {
        init();
        findAmazedMobi();

        bw.write(temp.size() + "\n");
        for (List<Integer> group : temp) {
            for (int i = 0; i < group.size(); i++) {
                if (i > 0) bw.write(" ");
                bw.write(group.get(i) + "");
            }
            bw.write("\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        M1 = Integer.parseInt(st.nextToken());
        M2 = Integer.parseInt(st.nextToken());
        M3 = Integer.parseInt(st.nextToken());

        uf = new int[3][N+1];
        size = new int[3][N+1];
        map = new HashMap<>();
        temp = new ArrayList<>();

        for (int i = 0; i < 3; i++) {
            for (int j = 1; j <= N; j++) {
                uf[i][j] = j;
                size[i][j] = 1;
            }
        }

        for (int i = 0; i < M1; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            union(a, b, 0);
        }

        for (int i = 0; i < M2; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            union(a, b, 1);
        }

        for (int i = 0; i < M3; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            union(a, b, 2);
        }
    }

    private static void findAmazedMobi() {
        Map<String, List<Integer>> groups = new HashMap<>();

        for (int node = 1; node <= N; node++) {
            String key = find(node, 0) + "," + find(node, 1) + "," + find(node, 2);

            groups.putIfAbsent(key, new ArrayList<>());
            groups.get(key).add(node);
        }

        for (List<Integer> group : groups.values()) {
            if (group.size() >= 2) {
                Collections.sort(group);
                temp.add(group);
            }
        }

        temp.sort((a, b) -> Integer.compare(a.get(0), b.get(0)));
    }

    private static void union(int x, int y, int index) {
        int X = find(x, index);
        int Y = find(y, index);

        if (size[index][X] < size[index][Y]) {
            uf[index][X] = Y;
            size[index][Y] += size[index][X];
        } else {
            uf[index][Y] = X;
            size[index][X] += size[index][Y];
        }
    }

    private static int find(int x, int index) {
        if (uf[index][x] == x) return x;

        return uf[index][x] = find(uf[index][x], index);
    }
}
```
