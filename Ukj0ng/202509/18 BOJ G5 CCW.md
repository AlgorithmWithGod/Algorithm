```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] points;
    private static int[] vector1, vector2;

    public static void main(String[] args) throws IOException {
        init();

        int answer = ccw();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        points = new int[3][2];

        for (int i = 0; i < 3; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            points[i][0] = Integer.parseInt(st.nextToken());
            points[i][1] = Integer.parseInt(st.nextToken());
        }

        vector1 = new int[2];
        vector2 = new int[2];

        vector1[0] = points[1][0] - points[0][0];
        vector1[1] = points[1][1] - points[0][1];

        vector2[0] = points[2][0] - points[1][0];
        vector2[1] = points[2][1] - points[1][1];
    }

    private static int ccw() {
        int crossProduct = vector1[0] * vector2[1] - vector1[1] * vector2[0];

        if (crossProduct > 0) {
            return 1;
        } else if (crossProduct < 0) {
            return -1;
        } else {
            return 0;
        }
    }
}
```
