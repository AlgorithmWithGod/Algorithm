```java
import java.sql.Array;
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;

    static int N, K = 0;
    static int[] len;

    public static void main(String[] args) throws Exception {

        input();
        solve();

    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        len = new int[100];
        len[1] = 5;
        len[2] = 13;
        for(int i=3;;i++) {
            len[i] = len[i-1] + len[i-2] + 1;
            K = i;
            if(len[i] >= N) break;
        }

        br.close();
    }

    public static void solve() throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        char res = get(K, N);
        bw.write((res == ' ' ? "Messi Messi Gimossi" : res) + "\n");

        bw.close();
    }

    public static char get(int n, int k) {
        if(n == 1) return "Messi".charAt(k-1);
        if(n == 2) return "Messi Gimossi".charAt(k-1);
        if(k == len[n-1] + 1) return ' ';
        if(k > len[n-1]) return get(n-2, k-len[n-1]-1);
        return get(n-1, k);
    }

}
```
