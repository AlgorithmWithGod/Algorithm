```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, -1, 0, 1};
    private static int[][] moves;
    private static int v, m, t, x, y;

    public static void main(String[] args) throws IOException {
        init();

        if (t > 1) {
            t--;
            int tempX = 0;
            int tempY = 0;
            for (int i = 0; i < 4; i++) {
                tempX += moves[i][0];
                tempY += moves[i][1];
            }
            int a = t/4;
            tempX *= a;
            tempY *= a;
            x += tempX;
            y += tempY;

            int b = t%4;
            for (int i = 0; i < b; i++) {
                x += moves[i][0];
                y += moves[i][1];
            }
        }

        bw.write(x + " " + y + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        v = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        t = Integer.parseInt(st.nextToken());

        moves = new int[4][2];

        x = 0;
        y = v;

        for (int i = 0; i < 4; i++) {
            moves[i][0] = dx[i]*(v*m)%10;
            moves[i][1] = dy[i]*(v*m)%10;
            v = (v*m)%10;
        }
    }
}
```
