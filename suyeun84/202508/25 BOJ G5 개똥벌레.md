```java
import java.util.*;
import java.io.*;

public class boj3020 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int H = nextInt();

        int[] A = new int[H + 1];
        int[] B = new int[H + 1];

        for (int n = 0; n < N; n += 2) {
            nextLine();
            A[nextInt()]++;
            nextLine();
            B[nextInt()]++;
        }

        for (int h = H - 1; 0 < h; h--) {
            A[h] += A[h + 1];
            B[h] += B[h + 1];
        }

        int count = 0;
        int min = N;

        for (int h = H; 0 < h; h--) {
            if (A[h] + B[H - h + 1] < min) {
                count = 1;
                min = A[h] + B[H - h + 1];
            } else if (A[h] + B[H - h + 1] == min) {
                count++;
            }
        }
        System.out.println(min + " " + count);
    }
}
```
