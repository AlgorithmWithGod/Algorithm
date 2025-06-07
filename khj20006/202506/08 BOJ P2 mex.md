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

class Node {
    Node left, right;
    Node() {
        left = null;
        right = null;
    }
}

class Trie {
    Node root;
    Trie(){
        root = new Node();
    }

    // 정수 x 삽입
    void insert(int x) {
        int k = 1<<18;
        Node now = root;
        while(k > 0) {
            int bit = x & k;
            if(bit == 0) {
                if(now.left == null) now.left = new Node();
                now = now.left;
            }
            else {
                if(now.right == null) now.right = new Node();
                now = now.right;
            }
            k >>= 1;
        }
    }

    // x와 XOR 했을 때의 최솟값 찾기
    int find(int x) {
        int k = 1<<18, res = 0;
        Node now = root;
        while(k > 0) {
            int bit = x & k;
            if(bit == 0) {
                if(now.left == null){
                    res |= k;
                    now = now.right;
                }
                else{
                    now = now.left;
                }
            }
            else {
                if(now.right == null) {
                    res |= k;
                    now = now.left;
                }
                else{
                    now = now.right;
                }
            }
            k >>= 1;
        }
        return res;
    }
}

public class Main {

    static IOController io;

    //

    static int N, M;
    static boolean[] exist;
    static Trie trie;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        exist = new boolean[524288];
        for(int i=1;i<=N;i++) exist[io.nextInt()] = true;

        trie = new Trie();
        for(int i=0;i<524288;i++) if(!exist[i]) trie.insert(i);

    }

    static void solve() throws Exception {

        int X = 0;
        for(int i=0;i<M;i++) {
            X ^= io.nextInt();
            io.write(trie.find(X) + "\n");
        }

    }


}
```
