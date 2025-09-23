```java
import java.io.*;
import java.util.*;

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
        while (!st.hasMoreTokens())
            nextLine();
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

    static long N;
    static TreeSet<Long> set = new TreeSet<>();

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextLong();
        set.add(1L);
        bck(1);
        io.write(set.size() + "\n");

        io.close();

    }

    static void bck(long s) {
        for(int i=2;i<=9;i++) if(s*i <= N) {
            if(!set.contains(s*i) && Long.toString(s*i).contains(Integer.toString(i))) {
                set.add(s*i);
                bck(s*i);
            }
        }
    }

}
```
