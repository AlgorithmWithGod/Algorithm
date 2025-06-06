```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController(){
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    void nextLine() throws Exception {
        st = new StringTokenizer(br.readLine());
    }

    String nextToken() throws Exception {
        while(!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
    long nextLong() throws Exception { return Long.parseLong(nextToken()); }
    double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Solution {

    static IOController io;

    //

    static int B, W, X, Y, Z;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        for(int T = io.nextInt();T-->0;solve()) input();

        io.close();

    }

    public static void input() throws Exception {

        B = io.nextInt();
        W = io.nextInt();
        X = io.nextInt();
        Y = io.nextInt();
        Z = io.nextInt();

    }

    static void solve() throws Exception {

        int res = -(int)1e9;
        for(int c=0;c<=Math.min(B,W);c++) {
            res = Math.max(res, B*X + W*Y - c*(X+Y) + 2*c*Z);
        }
        io.write(res + "\n");

    }


}
```
