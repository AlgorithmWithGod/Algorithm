```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

class Line {
    int s, e, num;
    Line(int s, int e, int num) {
        this.s = s;
        this.e = e;
        this.num = num;
    }
}

public class Main {

    static IOController io;

    //

    static int N, Q;
    static int[] r;
    static Line[] x, y;

    static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        Q = io.nextInt();
        x = new Line[N];
        y = new Line[N];
        r = new int[N];
        for(int i=0;i<N;i++) {
            r[i] = i;
            int x1 = io.nextInt();
            int y1 = io.nextInt();
            int x2 = io.nextInt();
            int y2 = io.nextInt();
            if(x1 > x2) {
                int tmp = x1;
                x1 = x2;
                x2 = tmp;
            }
            if(y1 > y2) {
                int tmp = y1;
                y1 = y2;
                y2 = tmp;
            }

            x[i] = new Line(x1, x2, i);
            y[i] = new Line(y1, y2, i);
        }

    }

    static void solve() throws Exception {

        connect(x);
        connect(y);
        while(Q-->0) {
            int a = f(io.nextInt()-1), b = f(io.nextInt()-1);
            io.write((a==b ? "1\n" : "0\n"));
        }

    }

    static void connect(Line[] arr) {
        Arrays.sort(arr, (a,b) -> a.s==b.s ? a.e-b.e : a.s-b.s);
        int max = arr[0].e, idx = arr[0].num;
        for(int i=1;i<arr.length;i++) {
            if(arr[i].s <= max) {
                int a = f(arr[i].num), b = f(idx);
                if(a != b) r[a] = b;
            }
            if(arr[i].e > max) {
                max = arr[i].e;
                idx = arr[i].num;
            }
        }
    }

}
```
