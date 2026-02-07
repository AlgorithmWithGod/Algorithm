```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Set<Long> visited;
    private static long N;

    public static void main(String[] args) throws IOException {
        init();

        DFS(N);
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Long.parseLong(br.readLine());
        visited = new HashSet<>();

        visited.add(0L);
        visited.add(1L);
        visited.add(2L);
    }

    private static void DFS(long target) throws IOException{
        if (visited.contains(target)) return;

        long x = (long)Math.sqrt(target);
        if (x*x < target) x++;

        long y = x*x - target;

        DFS(x);
        DFS(y);

        bw.write(x + " " + y + "\n");
        visited.add(target);
    }
}
```
