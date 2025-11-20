```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Set<String> visited;
    private static TreeSet<Integer> set;
    private static int A, B, C;
    public static void main(String[] args) throws IOException {
        init();
        BFS();

        for (Integer e : set) {
            bw.write(e + " ");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        A = Integer.parseInt(st.nextToken());
        B = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        visited = new HashSet<>();
        set = new TreeSet<>();


    }

    private static void BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        visited.add(0 + "," + 0 + "," + C);
        q.add(new int[]{0, 0, C});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == 0) {
                set.add(current[2]);
            }

            for (int i = 0; i < 3; i++) {
                if (i == 0 && current[0] > 0) {
                    int nB = Math.min(B, current[0] + current[1]);
                    int nA = current[0] - (nB - current[1]);

                    if (!visited.contains(nA + "," + nB + "," + current[2])) {
                        visited.add(nA + "," + nB + "," + current[2]);
                        q.add(new int[]{nA, nB, current[2]});
                    }

                    int nC = Math.min(C, current[0] + current[2]);
                    nA = current[0] - (nC - current[2]);
                    if (!visited.contains(nA + "," + current[1] + "," + nC)) {
                        visited.add(nA + "," + current[1] + "," + nC);
                        q.add(new int[]{nA, current[1], nC});
                    }
                } else if (i == 1 && current[1] > 0) {
                    int nA = Math.min(A, current[0] + current[1]);
                    int nB = current[1] - (nA - current[0]);

                    if (!visited.contains(nA + "," + nB + "," + current[2])) {
                        visited.add(nA + "," + nB + "," + current[2]);
                        q.add(new int[]{nA, nB, current[2]});
                    }

                    int nC = Math.min(C, current[1] + current[2]);
                    nB = current[1] - (nC - current[2]);
                    if (!visited.contains(current[0] + "," + nB + "," + nC)) {
                        visited.add(current[0] + "," + nB + "," + nC);
                        q.add(new int[]{current[0], nB, nC});
                    }
                } else if (i == 2 && current[2] > 0) {
                    int nA = Math.min(A, current[0] + current[2]);
                    int nC = current[2] - (nA - current[0]);

                    if (!visited.contains(nA + "," + current[1] + "," + nC)) {
                        visited.add(nA + "," + current[1] + "," + nC);
                        q.add(new int[]{nA, current[1], nC});
                    }

                    int nB = Math.min(B, current[1] + current[2]);
                    nC = current[2] - (nB - current[1]);
                    if (!visited.contains(current[0] + "," + nB + "," + nC)) {
                        visited.add(current[0] + "," + nB + "," + nC);
                        q.add(new int[]{current[0], nB, nC});
                    }
                }
            }
        }
    }
}
```
