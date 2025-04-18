```java
import java.io.*;
import java.util.*;

public class Main {

    static int r, c, starti = -1, startj = -1, endi, endj;
    static char[][] matrix;
    static boolean[][] check;
    static boolean[][] watercheck;
    static ArrayDeque<int[]> wq, sq;
    static int[] di = {-1, 1, 0, 0};
    static int[] dj = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        r = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());
        matrix = new char[r][c];
        check = new boolean[r][c];
        watercheck = new boolean[r][c];
        wq = new ArrayDeque<>();
        sq = new ArrayDeque<>();

        for (int i = 0; i < r; i++) {
            String line = br.readLine();
            for (int j = 0; j < c; j++) {
                matrix[i][j] = line.charAt(j);
                if (matrix[i][j] == 'L') {
                    if (starti == -1 && startj == -1) {
                        starti = i;
                        startj = j;
                    } else {
                        endi = i;
                        endj = j;
                    }
                    matrix[i][j] = '.';
                }

                if (matrix[i][j] == '.') {
                    wq.add(new int[] {i, j});
                    watercheck[i][j] = true;
                }
            }
        }

        sq.add(new int[] {starti, startj});
        check[starti][startj] = true;

        int time = 0;
        while (!move()) {
            melting();
            time++;
        }
        bw.write(time + "");
        bw.close();
    }

    public static boolean move() {
        ArrayDeque<int[]> q = new ArrayDeque<>();

        while (!sq.isEmpty()) {
            int[] cur = sq.poll();
            if (cur[0] == endi && cur[1] == endj) {
                return true;
            }

            for (int k = 0; k < 4; k++) {
                int newi = cur[0] + di[k];
                int newj = cur[1] + dj[k];

                if (newi < 0 || newi >= r || newj < 0 || newj >= c || check[newi][newj])
                    continue;

                check[newi][newj] = true;
                if (matrix[newi][newj] == '.') {
                    sq.add(new int[] {newi, newj});
                } else if (matrix[newi][newj] == 'X') {
                    q.add(new int[] {newi, newj});
                }
            }
        }

        sq = q;
        return false;
    }

    public static void melting() {
        int size = wq.size();
        for (int i = 0; i < size; i++) {
            int[] cur = wq.poll();

            for (int k = 0; k < 4; k++) {
                int newi = cur[0] + di[k];
                int newj = cur[1] + dj[k];

                if (newi < 0 || newi >= r || newj < 0 || newj >= c || watercheck[newi][newj])
                    continue;
                if (matrix[newi][newj] == 'X') {
                    matrix[newi][newj] = '.';
                    wq.add(new int[] {newi, newj});
                    watercheck[newi][newj] = true;
                }
            }
        }
    }
}

```
