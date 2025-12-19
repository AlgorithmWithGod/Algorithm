```java
import java.sql.Array;
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static int N, K;
    static String[] arr;
    static boolean[] exist;

    public static void main(String[] args) throws Exception {

        input();
        solve();

    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        arr = new String[N];
        exist = new boolean[1<<K];
        for(int i=0;i<N;i++) arr[i] = br.readLine();

        br.close();
    }

    public static void solve() throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int Z = 0;
        for(int i=0;i<N;i++) {
            if(Z == 1) {
                String rev = "";
                for(int j=K-1;j>=0;j--) rev += arr[i].charAt(j);
                arr[i] = rev;
            }
            int a = Integer.parseInt(arr[i], 2);
            if(exist[a]) {
                bw.write("WellKnown\n");
                Z = 0;
            }
            else {
                bw.write("AdHoc\n");
                Z = 1;
            }
            bck(a);
        }

        bw.close();
    }

    public static void bck(int a) {
        if(exist[a]) return;
        exist[a] = true;
        for(int i=0;i<K;i++) if((a & (1<<i)) != 0) {
            bck(a ^ (1<<i));
        }
    }

}
```
