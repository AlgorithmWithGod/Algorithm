```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<Integer, Integer> result;
    private static int[] power, uf, size;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();

        for (int i = 1; i <= N; i++) {
            int root = find(i);

            if (!result.containsKey(root) && power[root] > 0) {
                result.put(root, power[root]);
            }
        }

        bw.write(result.size() + "\n");

        List<Integer> value = new ArrayList<>(result.values());
        Collections.sort(value);

        for (int element : value) {
            bw.write(element + " ");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        power = new int[N+1];
        uf = new int[N+1];
        size = new int[N+1];

        result = new HashMap<>();

        for (int i = 1; i <= N; i++) {
            power[i] = Integer.parseInt(br.readLine());
            uf[i] = i;
            size[i] = 1;
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int O = Integer.parseInt(st.nextToken());
            int P = Integer.parseInt(st.nextToken());
            int Q = Integer.parseInt(st.nextToken());

            union(P, Q, O);
        }
    }

    private static void union(int x, int y, int o) {
        int X = find(x);
        int Y = find(y);

        if (o == 1) {
            if (size[X] < size[Y]) {
                uf[X] = Y;
                size[Y] += size[X];
                power[Y] += power[X];

            } else {
                uf[Y] = X;
                size[X] += size[Y];
                power[X] += power[Y];
            }
        } else {
            if (power[X] == power[Y]) {
                power[X] = 0;
                power[Y] = 0;
            } else if (power[X] > power[Y]) {
                uf[Y] = X;
                size[X] += size[Y];
                power[X] -= power[Y];
            } else {
                uf[X] = Y;
                size[Y] += size[X];
                power[Y] -= power[X];
            }
        }
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }
}
```
