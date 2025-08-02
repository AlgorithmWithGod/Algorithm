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

    static int N;
    static long R;
    static int[][] a;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        R = io.nextLong();
        a = new int[N][N];
        for(int i=0;i<N;i++) for(int j=0;j<N;j++) a[i][j] = io.nextInt();

    }

    static void solve() throws Exception {

        // 불가능한 경우 판별
        {
            long max = 0;
            for(int i=0;i<N;i++) for(int j=0;j<N;j++) max = Math.max(max, a[i][j]);
            if(max*N*N < R) {
                io.write("-1");
                return;
            }
        }

        int s = 1, e = N, m = (s+e)>>1;
        while(s<e) {

            int K = m;
            int[][] row = new int[N][N];
            int[][] rowMax = new int[N][N];
            Deque<int[]>[] deques = new Deque[N];
            for(int i=0;i<N;i++) deques[i] = new ArrayDeque<>();

            for(int i=0;i<N;i++) {
                Deque<int[]> deque = new ArrayDeque<>();
                for(int j=0;j<K-1;j++) {
                    while(!deque.isEmpty() && deque.peekLast()[0] < a[i][j]) deque.pollLast();
                    deque.offerLast(new int[]{a[i][j], j});
                }
                for(int j=0;j<N;j++) {
                    if(j+K-1 < N) {
                        while(!deque.isEmpty() && deque.peekLast()[0] < a[i][j+K-1]) deque.pollLast();
                        deque.offerLast(new int[]{a[i][j+K-1], j+K-1});
                    }
                    while(!deque.isEmpty() && deque.peekFirst()[1] < j) deque.pollFirst();
                    row[i][j] = deque.peekFirst()[0];

                    //

                    while(!deques[j].isEmpty() && deques[j].peekLast()[0] < row[i][j]) deques[j].pollLast();
                    deques[j].offerLast(new int[]{row[i][j], i});
                    while(!deques[j].isEmpty() && i - deques[j].peekFirst()[1] >= K) deques[j].pollFirst();
                    if(i >= K-1) rowMax[i-K+1][j] = deques[j].peekFirst()[0];

                }
            }
            for(int i=N-K+1;i<N;i++) for(int j=0;j<N;j++) {
                while(!deques[j].isEmpty() && deques[j].peekFirst()[1] < i) deques[j].pollFirst();
                rowMax[i][j] = deques[j].peekFirst()[0];
            }

            int[][] col = new int[N][N];
            int[][] colMax = new int[N][N];
            deques = new Deque[N];
            for(int i=0;i<N;i++) deques[i] = new ArrayDeque<>();

            for(int j=0;j<N;j++) {
                Deque<int[]> deque = new ArrayDeque<>();
                for(int i=0;i<K-1;i++) {
                    while(!deque.isEmpty() && deque.peekLast()[0] < a[i][j]) deque.pollLast();
                    deque.offerLast(new int[]{a[i][j], i});
                }
                for(int i=0;i<N;i++) {
                    if(i+K-1 < N) {
                        while(!deque.isEmpty() && deque.peekLast()[0] < a[i+K-1][j]) deque.pollLast();
                        deque.offerLast(new int[]{a[i+K-1][j], i+K-1});
                    }
                    while(!deque.isEmpty() && deque.peekFirst()[1] < i) deque.pollFirst();
                    col[i][j] = deque.peekFirst()[0];

                    //

                    while(!deques[i].isEmpty() && deques[i].peekLast()[0] < col[i][j]) deques[i].pollLast();
                    deques[i].offerLast(new int[]{col[i][j], j});
                    while(!deques[i].isEmpty() && j - deques[i].peekFirst()[1] >= K) deques[i].pollFirst();
                    if(j >= K-1) colMax[i][j-K+1] = deques[i].peekFirst()[0];
                }
            }
            for(int i=0;i<N;i++) for(int j=N-K+1;j<N;j++) {
                while(!deques[i].isEmpty() && deques[i].peekFirst()[1] < j) deques[i].pollFirst();
                colMax[i][j] = deques[i].peekFirst()[0];
            }

            long res = 0;
            for(int i=0;i<N;i++) for(int j=0;j<N;j++) res += Math.max(rowMax[i][j], colMax[i][j]);

            if(res >= R) e = m;
            else s = m+1;
            m = (s+e)>>1;

        }
        io.write(m + "\n");

    }

}
```
