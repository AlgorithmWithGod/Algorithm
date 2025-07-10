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

public class Main {

    static IOController io;

    //

    static char[] a;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();
    }

    public static void init() throws Exception {

        a = io.nextLine().toCharArray();

    }

    static void solve() throws Exception {

        Deque<String> d = new ArrayDeque<>();
        for(int i=0;i<a.length;i++) d.offerLast(Character.toString(a[i]));
        io.write(get(d));

    }

    static String get(Deque<String> d) {
        Deque<String> d1 = new ArrayDeque<>();
        while(!d.isEmpty()) {
            String a = d.pollFirst();
            if(a.equals(")")) {
                String last;
                Deque<String> temp = new ArrayDeque<>();
                while(!(last = d1.pollLast()).equals("(")) temp.offerFirst(last);
                d1.addLast(get(temp));
            }
            else d1.addLast(a);
        }

        Deque<String> d2 = new ArrayDeque<>();
        while(!d1.isEmpty()) {
            String a = d1.pollFirst();
            if(d2.isEmpty()) {
                d2.addLast(a);
                continue;
            }
            String last = d2.peekLast();
            if(last.equals("*") || last.equals("/")) {
                d2.pollLast();
                String llast = d2.pollLast();
                d2.addLast(llast + a + last);
            }
            else d2.addLast(a);
        }

        Deque<String> d3 = new ArrayDeque<>();
        while(!d2.isEmpty()) {
            String a = d2.pollFirst();
            if(d3.isEmpty()) {
                d3.addLast(a);
                continue;
            }
            String last = d3.peekLast();
            if(last.equals("+") || last.equals("-")) {
                d3.pollLast();
                String llast = d3.pollLast();
                d3.addLast(llast + a + last);
            }
            else d3.addLast(a);
        }

        return d3.poll();
    }

}
```
