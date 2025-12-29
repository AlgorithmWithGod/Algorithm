```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 1, -1, -1};
    private static final int[] dy = {1, -1, 1, -1};
    private static List<int[]> nets, fishes;
    private static boolean[][] map;
    private static int N, I, M, answer;

    public static void main(String[] args) throws IOException {
        init();

        for (int[] pos : fishes){
            for (int[] net : nets) {
                for (int i = pos[0]-net[0]; i <= pos[0]+net[0]; i++) {
                    int count = 0;
                    for (int[] fish : fishes) {
                        if (i <= fish[0] && fish[0] <= i+net[0] && pos[1] <= fish[1] && fish[1] <= pos[1]+net[1]) count++;
                    }
                    answer = Math.max(answer, count);
                }

                for (int i = pos[1]-net[1]; i <= pos[1]+net[1]; i++) {
                    int count = 0;
                    for (int[] fish : fishes) {
                        if (i <= fish[1] && fish[1] <= i+net[1] && pos[0] <= fish[0] && fish[0] <= pos[0]+net[0]) count++;
                    }
                    answer = Math.max(answer, count);
                }
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        I = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new boolean[N+1][N+1];
        fishes = new ArrayList<>();

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            map[x][y] = true;
            fishes.add(new int[]{x, y});
        }

        nets = makeNet();
    }

    private static List<int[]> makeNet() {
        List<int[]> nets = new ArrayList<>();

        int r = 1;
        int c = I/2-1;

        while (c > 0) {
            nets.add(new int[]{r, c});
            r++;
            c--;
        }

        return nets;
    }

    private static boolean OOB(int x, int y) {
        return x < 1 || x > N || y < 1 || y > N;
    }
}
```
