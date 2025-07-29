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

enum Status {
    BEFORE, LINE, CIRCLE, AFTER
}

public class Main {

    static IOController io;

    //

    static int N, M;
    static int[][] edges;
    static int[] r;
    static Status[] s;
    static List<Integer>[] graph;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

    static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        edges = new int[M][];
        for(int i=0;i<M;i++) edges[i] = new int[]{io.nextInt(),io.nextInt(),io.nextInt()};
        r = new int[N+1];
        s = new Status[N+1];
        graph = new List[N+1];
        for(int i=1;i<=N;i++) {
            r[i] = i;
            s[i] = Status.BEFORE;
            graph[i] = new ArrayList<>();
        }

    }

    static void solve() throws Exception {

        Arrays.sort(edges, (a,b) -> b[2]-a[2]);

        int ans = edges[0][2], val = Integer.MAX_VALUE, idx = 0;
        int lines = 0, circles = 0;
        // weight sweeping
        while(idx < M) {
            int currentWeight = edges[idx][2];
            while(idx < M && edges[idx][2] == currentWeight) {
                int a = edges[idx][0], b = edges[idx][1];
                int x = f(a), y = f(b);
                if(x == y) {
                    if(s[x] == Status.CIRCLE) {
                        circles--;
                        s[x] = Status.AFTER;
                    }
                    else if(s[x] == Status.LINE) {
                        lines--;
                        if(graph[a].size() > 1 || graph[b].size() > 1) {
                            s[x] = Status.AFTER;
                        }
                        else {
                            circles++;
                            s[x] = Status.CIRCLE;
                        }
                    }
                }
                else {
                    if(s[x] == Status.BEFORE) {
                        r[x] = y;
                        if(s[y] == Status.BEFORE) {
                            lines++;
                            s[y] = Status.LINE;
                        }
                        else if(s[y] == Status.LINE) {
                            if(graph[b].size() > 1) {
                                lines--;
                                s[y] = Status.AFTER;
                            }
                        }
                        else if(s[y] == Status.CIRCLE) {
                            circles--;
                            s[y] = Status.AFTER;
                        }
                    }
                    else if(s[x] == Status.LINE) {
                        r[y] = x;
                        if(s[y] == Status.BEFORE) {
                            if(graph[a].size() > 1) {
                                lines--;
                                s[x] = Status.AFTER;
                            }
                        }
                        else if(s[y] == Status.LINE) {
                            lines--;
                            if(graph[a].size() > 1 || graph[b].size() > 1) {
                                lines--;
                                s[x] = Status.AFTER;
                            }
                        }
                        else if(s[y] == Status.CIRCLE) {
                            circles--;
                            lines--;
                            s[x] = Status.AFTER;
                        }
                        else {
                            lines--;
                            s[x] = Status.AFTER;
                        }
                    }
                    else if(s[x] == Status.CIRCLE) {
                        r[y] = x;
                        if(s[y] == Status.BEFORE) {
                            circles--;
                            s[x] = Status.AFTER;
                        }
                        else if(s[y] == Status.LINE) {
                            lines--;
                            circles--;
                            s[x] = Status.AFTER;
                        }
                        else if(s[y] == Status.CIRCLE) {
                            circles-=2;
                            s[x] = Status.AFTER;
                        }
                        else {
                            circles--;
                            s[x] = Status.AFTER;
                        }
                    }
                    else {
                        r[y] = x;
                        if(s[y] == Status.LINE) {
                            lines--;
                        }
                        else if(s[y] == Status.CIRCLE) {
                            circles--;
                        }
                    }
                    graph[a].add(b);
                    graph[b].add(a);
                }
                idx++;
            }

            int res = Math.abs(lines-circles);
            if(res <= val) {
                ans = currentWeight;
                val = res;
            }

        }

        io.write(ans + " " + val);

    }

}
```
