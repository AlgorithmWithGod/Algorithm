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
    long a, b;
    Line(long a, long b) {
        this.a = a;
        this.b = b;
    }
    long get(long x) {
        return a*x + b;
    }
}

class Node {
    int l, r;
    long s, e;
    Line line;
    Node(long s, long e, Line line) {
        this.l = -1;
        this.r = -1;
        this.s = s;
        this.e = e;
        this.line = line;
    }
}

class LiChao {
    List<Node> tree;
    LiChao(long s, long e) {
        tree = new ArrayList<>();
        tree.add(new Node(s, e, new Line(0, -(long)1e18-1)));
    }

    void update(int n, Line line) {
        long s = tree.get(n).s, e = tree.get(n).e, m = (s+e)>>1;

        Line low = tree.get(n).line, high = line;
        if(low.get(s) > high.get(s)) {
            low = line;
            high = tree.get(n).line;
        }

        if(low.get(e) <= high.get(e)) {
            tree.get(n).line = high;
            return;
        }

        if(low.get(m) <= high.get(m)) {
            tree.get(n).line = high;
            if(tree.get(n).r == -1) {
                tree.get(n).r = tree.size();
                tree.add(new Node(m+1,e,new Line(0, -(long)1e18-1)));
            }
            update(tree.get(n).r, low);
        }
        else {
            tree.get(n).line = low;
            if(tree.get(n).l == -1) {
                tree.get(n).l = tree.size();
                tree.add(new Node(s,m,new Line(0, -(long)1e18-1)));
            }
            update(tree.get(n).l, high);
        }
    }

    long query(int n, long x) {
        if(n == -1) return -(long)1e18 - 1;
        long s = tree.get(n).s, e = tree.get(n).e, m = (s+e)>>1;
        long v = tree.get(n).line.get(x);
        if(x <= m) return Math.max(v, query(tree.get(n).l, x));
        return Math.max(v, query(tree.get(n).r, x));
    }
}

public class Main {

    static IOController io;

    //

    static int Q;
    static LiChao tree;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        Q = io.nextInt();
        tree = new LiChao(-(long)1e12, (long)1e12);

    }

    static void solve() throws Exception {

        while(Q-->0) {
            int op = io.nextInt();

            if(op == 1) {
                long a = io.nextLong();
                long b = io.nextLong();
                tree.update(0, new Line(a,b));
            }
            else {
                long x = io.nextLong();
                io.write(tree.query(0, x) + "\n");
            }

        }

    }

}
```
