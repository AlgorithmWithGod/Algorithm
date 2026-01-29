```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int N, r, c, count, answer;

    public static void main(String[] args) throws IOException {
        init();

        DFS(0, 0, (int)Math.pow(2, N));

        bw.write(answer + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        r = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());
        count = 0;
    }

    private static void DFS(int x, int y, int size) {
        if (size == 1) {
            if (x == r && y == c) answer = count;
            count++;
            return;
        }

        if (r < x+size/2 && c < y+size/2) {
            DFS(x, y, size/2);
        } else if (r < x+size/2 && c < y+size) {
            count += size/2*size/2;
            DFS(x, y+size/2, size/2);
        } else if (r < x+size && c < y+size/2) {
            count += size/2*size/2*2;
            DFS(x+size/2, y, size/2);
        } else {
            count += size/2*size/2*3;
            DFS(x+size/2, y+size/2, size/2);
        }
    }
}
```
