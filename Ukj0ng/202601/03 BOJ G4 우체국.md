```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] villages;
    private static int N;
    private static long sum;

    public static void main(String[] args) throws IOException {
        init();

        long temp = 0;
        int answer = 0;
        for (int i = 0; i < N; i++) {
            temp += villages[i][1];

            if (temp >= (sum+1)/2) {
                answer = villages[i][0];
                break;
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        villages = new int[N][2];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken());
            villages[i][0] = x;
            villages[i][1] = a;

            sum += a;
        }

        Arrays.sort(villages, (o1, o2) -> Integer.compare(o1[0], o2[0]));
    }
}
```
