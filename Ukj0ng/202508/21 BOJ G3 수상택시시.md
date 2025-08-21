```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> reverse;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        if (reverse.isEmpty()) {
            bw.write(M + "\n");
        } else {
            reverse.sort((o1, o2) -> {
                if (o1[0] == o2[0]) return Integer.compare(o1[1], o2[1]);
                return Integer.compare(o1[0], o2[0]);
            });

            List<int[]> list = new ArrayList<>();
            int[] current = reverse.get(0);

            for (int i = 1; i < reverse.size(); i++) {
                int[] next = reverse.get(i);
                if (current[1] >= next[0]) {
                    current[1] = Math.max(current[1], next[1]);
                } else {
                    list.add(new int[]{current[0], current[1]});
                    current = next;
                }
            }

            list.add(current);

            long temp = M;

            for (int[] element : list) {
                temp += (element[1] - element[0]) * 2L;
            }

            bw.write(temp + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        reverse = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            if (x > y) {
                reverse.add(new int[]{y, x});
            }
        }
    }
}

```
