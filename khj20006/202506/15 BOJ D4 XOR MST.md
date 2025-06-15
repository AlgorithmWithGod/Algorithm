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

class Node {
    int count;
    Node left, right;
    Node(){ count = 0; }
}

class Trie {
    Node root;
    Trie(){ root = new Node(); }

    void insert(int x) {
        Node now = root;
        int bit = 1<<29;
        while(bit > 0) {
            int val = x & bit;
            if(val == 0) {
                if(now.left == null) now.left = new Node();
                now = now.left;
            }
            else {
                if(now.right == null) now.right = new Node();
                now = now.right;
            }
            now.count++;
            bit >>= 1;
        }
    }

    void erase(int x) {
        Node now = root;
        eraseDfs(now, x, 1<<29);
    }

    boolean eraseDfs(Node now, int x, int bit) {
        if(bit == 0) return --now.count == 0;
        int val = x & bit;
        if(val == 0) {
            if(eraseDfs(now.left, x, bit>>1)) now.left = null;
        }
        else {
            if(eraseDfs(now.right, x, bit>>1)) now.right = null;
        }
        return --now.count == 0;
    }

}

public class Main {

    static IOController io;

    //

    static int N;
    static int[] A;
    static Trie P, Q;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        A = new int[N];
        for(int i=0;i<N;i++) A[i] = io.nextInt();
        P = new Trie();
        Q = new Trie();

    }

    static void solve() throws Exception {

        P.insert(A[0]);
        for(int i=1;i<N;i++) Q.insert(A[i]);

        long mst = 0;
        for(int i=1;i<N;i++) mst += set();

        io.write(mst + "\n");

    }

    static int set() {
        int[] result = find(P.root, Q.root, 1<<29);
        int cost = result[0], val = result[1];
        Q.erase(val);
        P.insert(val);
        return cost;
    }

    static int[] find(Node p, Node q, int bit) {

        if(bit == 0) return new int[]{0,0};

        boolean c1 = p.left != null && q.left != null;
        boolean c2 = p.right != null && q.right != null;
        boolean c3 = p.left != null && q.right != null;
        boolean c4 = p.right != null && q.left != null;

        if(c1 || c2) {
            if(c1 && c2) {
                int[] res1 = find(p.left, q.left, bit>>1);
                int[] res2 = find(p.right, q.right, bit>>1);
                res2[1] |= bit;
                if(res1[0] > res2[0]) return res2;
                return res1;
            }
            if(c1) return find(p.left, q.left, bit>>1);
            int[] res = find(p.right, q.right, bit>>1);
            res[1] |= bit;
            return res;
        }
        if(c3 && c4) {
            int[] res1 = find(p.left, q.right, bit>>1);
            res1[0] |= bit;
            res1[1] |= bit;
            int[] res2 = find(p.right, q.left, bit>>1);
            res2[0] |= bit;
            if(res1[0] > res2[0]) return res2;
            return res1;
        }
        if(c3) {
            int[] res = find(p.left, q.right, bit>>1);
            res[0] |= bit;
            res[1] |= bit;
            return res;
        }
        int[] res = find(p.right, q.left, bit>>1);
        res[0] |= bit;
        return res;

    }

}
```
