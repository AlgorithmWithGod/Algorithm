```java
import java.io.*;
import java.util.*;

public class boj1111 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        nextLine();
        int[] num = new int[N];
        for (int i = 0; i < N; i++) num[i] = nextInt();
        if (N == 1) {
            System.out.println("A");
            return;
        } else if (N == 2) {
            if (num[0] == num[1]) System.out.println(num[0]);
            else System.out.println("A");
            return;
        }
        int a = (num[1] != num[0]) ? (num[2] - num[1]) / (num[1] - num[0]) : 0;
        int b = num[1] - num[0] * a;

        for (int i = 1; i < N-1; i++) {
            if (num[i] * a + b != num[i+1]) {
                System.out.println("B");
                return;
            }
        }
        System.out.println(num[N-1] * a + b);
    }
}
```
