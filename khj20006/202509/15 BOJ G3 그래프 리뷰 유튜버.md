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

    static int N;
    static int[] c;
    static List<Integer>[] graph;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        c = new int[N+1];
        graph = new List[N+1];
        for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();

        for(int i=1;i<N;i++) {
            int a = io.nextInt();
            int b = io.nextInt();
            c[a]++;
            c[b]++;
            graph[a].add(b);
            graph[b].add(a);
        }

        for(int i=1;i<=N;i++) if(c[i] >= 3) {
            int a = graph[i].get(0);
            int b = graph[i].get(1);
            int c = graph[i].get(2);
            io.write("3\n");
            io.write(a + " " + b + "\n");
            io.write(b + " " + c + "\n");
            io.write(a + " " + c + "\n");
            io.close();
            return;
        }

        for(int i=1;i<=N;i++) for(int j:graph[i]) {
            if(c[i] == 2 && c[j] == 2) {
                int a = graph[i].get(0);
                if(a == j) a = graph[i].get(1);
                int b = graph[j].get(0);
                if(b == i) b = graph[j].get(1);
                io.write("3\n");
                io.write(a + " " + b + "\n");
                io.write(a + " " + j + "\n");
                io.write(b + " " + i + "\n");
                io.close();
                return;
            }
        }

    }

}
```
